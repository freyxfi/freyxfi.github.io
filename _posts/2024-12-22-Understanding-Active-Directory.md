---
title: "Understanding Active Directory and Duplicates"
date: 2024-12-22 20:19:00 +0800
categories: [Active Directory]
tags: [Tutorial, Active Directory]
image:
  path: https://i.pinimg.com/originals/a5/d1/f6/a5d1f61e89bdce061817723044f8a757.gif
---

# What Happened This Week?

Good day, everyone! I hope you are all doing well on the other side of the screen!

Starting in 2025, I plan to name weekly blog posts numerically, such as `#1 Week One` and `#2 Week Two`, and so on. 

This week was interesting, but it went slower than I expected. I didn’t do much hunting, worked on an Active Directory (AD) report for the company, but I guess it wasn’t up to the mark. The report listed 400-700 findings, typical for pentesting. However, if you look closely, it mostly highlights around 10 critical and high vulnerabilities.

# What Did I Do This Week?

- Led the company’s weekly talk.
- Hunted for just 1 hour (lol).
- Got a duplicate report.
- Started learning about Active Directory.
- Removed my AD environment.
- Skipped CTFs this week, but...
- Trained hard in MMA.
- Visited my village.

# Company Group Presentation

This week, I was selected to deliver a topic at the weekly company summit. As you know, I love to share and talk (maybe a bit too much!), so I volunteered to lead the session. I presented on Broken Access Control. If you’ve read my previous blogs, you’ll know the backstory about why I chose this topic.

The fun part is that I created a cool presentation, which I’ve shared on my Telegram. You can check it out [here](https://t.me/frx3y/362). Let me know how you like it! I’ll also be creating a YouTube video on it soon.

# Hunting Adventures

So, I only hunted for an hour this week but found an interesting bug. Here’s how it went down:

1. I was scrolling through a website and noticed it had a GPT feature.
2. I tried it and said “hello.”
3. It responded, “You have 9 prompts remaining for today.”
4. I thought, "Who are you to limit me?" 😂
5. The GPT responses were fun, so I decided to break the limit.
6. I intercepted the requests and found my `message_ID = xxxxxxxxxx1`.
7. I reused the same `message_ID` in the next response, and it worked!
8. I kept sending more prompts—up to 20—without any restrictions.
9. I quickly wrote a report, but...
10. I got a duplicate report and a kick in the *you-know-what* as a reward, haha!
11. Not surprised—it was right there on the main page, so other hunters likely spotted it too.

# Active Directory Adventures

As a red teamer, mastering Active Directory is essential—it’s the backbone of many organizations. My company had two pentesting projects this week: one focused on web attacks and the other on AD environments.

I performed well in web testing as it was highly vulnerable (admin emails leaked everywhere, allowing access to both the admin and Django panels). However, AD was a completely different story. 

Here’s how it went:
- I missed the initial hacking session due to being unwell.
- My team had already gained access to the Domain Controller (DC), but no connected computers were provided for testing.
- I performed a Kerberoasting attack and got credentials for 4 users, but replicating attacks like Golden Ticket was tough.
- Due to lack of resources and storage issues, I couldn’t progress much.

This experience taught me that running tools and getting usernames/passwords is one thing, but understanding the structure and inner workings of AD is crucial. 

# The Plan

To truly understand and break AD, I plan to start from scratch. In upcoming blogs, I’ll cover:

1. What is Active Directory?
2. Why do we need Active Directory?
3. How to set up Active Directory.
4. Structure of AD.
5. AD Terminology.
6. Authentication in AD.
7. Kerberos.
8. DNS.
9. LDAP.

In the next part, I’ll dive into attacks based on my PEN-200 notes. 

---


# What is Active Directory?

Active Directory (AD) is a service for Windows that provides authentication and authorization functionality within Windows domains. I think this is the best definition for it.

---

## Why Do We Need AD?

In large companies, organizing and managing computers is a challenge. While it's possible to manage 5–10 computers manually (or even 20 if you're experienced), managing 300–1,000 computers becomes impractical without a centralized system. This is where Active Directory comes in, making it essential for large-scale IT environments.

---

## How to Set Up AD?

Currently, I lack the space and resources to set up my own AD (I barely have 10GB of free space as I write this). However, I can explain the process:

1. Use a Windows Server as the domain controller (DC).
2. Connect 2 or more Windows machines to the DC.
3. Optionally, create a forest, which adds complexity.

Setting up AD is straightforward, but managing it can be challenging. This complexity often leads to misconfigurations, making AD a favorite target for hackers.

---

## Structure of AD

Active Directory has an interesting history, evolving with new features and vulnerabilities over time. Let’s look at its structure using an example: **STARK.local** (inspired by Stark Industries because Iron Man is my favorite hero).

### Key Components:
- **Root Domain:** For example, `stark.local`.
- **Tree Domain/Child Domain:** Subdomains under the root domain.
- **Objects:** Includes computers, users, groups, printers, etc.
- **Forest:** A connection of multiple domains, such as `stark.local` and `avenger.local`.

A forest can grow significantly larger with subtrees and other structures.

For a detailed breakdown of AD objects, see this image:  
[AD Objects - Hack The Box Academy](https://academy.hackthebox.com/storage/modules/74/adobjects.png).

Hack The Box Academy is an excellent resource for learning more!

---

## AD Terminology

Here’s a breakdown of common Active Directory terms:

1. **Object:** Anything within AD.
2. **Attribute:** Defines the characteristics of an object.
3. **Schema:** A blueprint of AD.
4. **Domain:** The topmost group in AD.
5. **Forest:** A collection of multiple trees.
6. **Tree:** A collection of multiple domains with the same root.
7. **Container:** Holds other objects.
8. **Leaf:** The last element in the AD hierarchy.
9. **GUID (Globally Unique Identifier):** Used to uniquely identify objects (similar to UUID).
10. **Security Principles:** Anything the system can authenticate.
11. **Distinguished Name (DN):** The full path of an object.
12. **Security Identifier (SID):** A unique ID issued by the domain controller.
13. **Relative Distinguished Name (RDN):** Differentiates objects with the same name.
14. **SAM Account Name:** User login name.
15. **User Principal Name (UPN):** A login name with `@` (e.g., `tony@stark.local`).
16. **FSMO Roles:** Five important roles assigned during setup; reassigning them can be complex.
17. **Global Catalog:** Keeps a copy of all objects in AD.
18. **Read-Only Domain Controller (RODC):** A read-only DC with no cached passwords.
19. **Replication:** Moving objects between domain controllers.
20. **Service Principal Name (SPN):** Identifies service instances used by Kerberos.
21. **Group Policy Object (GPO):** Contains local file system policies.
22. **Access Control List (ACL):** Access control rules for objects.
23. **Discretionary Access Control List (DACL):** Grants or denies access to objects.
24. **System Access Control List (SACL):** Logs system access.
25. **Fully Qualified Domain Name (FQDN):** The complete name of a host.
26. **Tombstone:** Stores deleted objects.
27. **AD Recycle Bin:** Restores deleted objects (not available in early versions of AD).
28. **Sysvol:** Shared public files (often targeted by attackers).
29. **AdminSD Holder:** Manages ACLs for privileged accounts.
30. **dsHeuristics:** Forest configuration settings.
31. **AdminCount:** Indicates administrative accounts (attackers often target this).
32. **Active Directory Users and Computers (ADUC):** A GUI for management.
33. **ADSI Edit:** Another GUI tool similar to ADUC.
34. **SID History:** Previous SIDs assigned to an object.
35. **NTDS.DIT:** A critical database containing passwords and other data.
36. **MSBROWSE:** A master browser.

---

## Summary
Active Directory is a powerful tool for managing Windows environments but comes with inherent complexities and security risks. I’ve covered key terminology, setup processes, and its structure, along with tips to dive deeper into the topic. I feel confident about understanding almost everything here! But this will go way beyond this 

# Kerberos Authentication 

Kerberos authentication is both fascinating and complex—like taking validation from your ex-girlfriend for a party! (Don't judge me, I never had a girlfriend, but hey, we can always imagine stuff!)

### Overview 
Kerberos authentication operates differently from NTLM as it uses a ticket-based mechanism. Here are some quick facts:  
- Kerberos has been Microsoft's primary authentication protocol since Windows Server 2003 (or 2000, according to Hack The Box).  
- It's stateless and highly secure if implemented correctly.  

### Steps in Kerberos Authentication

1. **Authentication Service Request**:  
   - When a user logs in, the client sends an **Authentication Service Request (AS-REQ)** to the Domain Controller (DC) or Key Distribution Center (KDC).  
   - This request includes the username, password (hashed), and a timestamp for validation.  
   - If the timestamp isn't a duplicate, the KDC encrypts it and proceeds.

2. **Authentication Service Reply**:  
   - The KDC responds with an **Authentication Service Reply (AS-REP)**, which includes a Ticket Granting Ticket (TGT) and a session key.  
   - The TGT contains information about the user (IP address, domain, groups, etc.).  
   - At this point, the user's identity is authenticated.

3. **Accessing Resources - Ticket Granting Service Request**:  
   - When a user tries to access a resource, they send a **Ticket Granting Service Request (TGS-REQ)** to the KDC.  
   - This request includes the TGT and the requested **Service Principal Name (SPN)**.  
   - The SPN is decrypted using the secret key known only to the KDC.

4. **Service Ticket Reply**:  
   - After verifying the request, the KDC sends a **Ticket Granting Service Reply (TGS-REP)**, which includes the service ticket, session key, and SPN.  
   - The service ticket contains new session details and group information.  
   - Once the client has the session ticket and key, the actual **service authentication begins**.

### Summary 
Kerberos is simple in concept but challenging to implement correctly due to its intricacies. The entire process relies on encrypted communication, session keys, and tickets for secure authentication and resource access.

---

### Join My Discord Server!  
Hey, before you go, consider joining my newly created Discord server!  
[https://discord.gg/aBCx4hFfpk](https://discord.gg/aBCx4hFfpk)