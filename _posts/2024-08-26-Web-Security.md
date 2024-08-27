---
title: "Web Security on Fire" 
date: 2024-08-26 00:00:00 +0800
categories: [Web Security]
tags: [Web, Security, offsec]
---

## Web Security

As I am really into web security in 2024, I spend most of my day testing random sites. This article serves as a starting point where I'll take you through my journey of findings and all the testing I've done so far.

### Starting Point

Yes, we do have a starting point here, and that's what we call the **OWASP Top Ten**—ring any bells? That's what we're focusing on so far. I'll make sure to cover all of these and then write a detailed article on each one of them.

But why am I doing this? I wasn't always into web security—so why now? Well, the thing is, I've always wanted to dig deeper into web security, specifically in the realm of Web 2.0, to explore all the awesome companies and discover bugs. Sometimes I report them, sometimes I don't.

### OWASP TOP 10

1. **Broken Access Control**  
   Improperly implemented access controls can allow unauthorized access to user accounts or sensitive information. This is one of the most common and critical vulnerabilities.

2. **Cryptographic Failures**  
   Previously known as Sensitive Data Exposure, this refers to failures in protecting sensitive data through encryption and other cryptographic means.

3. **Injection**  
   This includes SQL, NoSQL, Command Injection, and others, where untrusted data is sent to an interpreter as part of a command or query.

4. **Insecure Design**  
   This involves the lack of security considerations during the design phase, leading to inherent vulnerabilities in the application.

5. **Security Misconfiguration**  
   This is the most commonly seen issue. It can occur at any level of an application stack, and often happens when security settings are not defined, implemented, or maintained properly.

6. **Vulnerable and Outdated Components**  
   Using components with known vulnerabilities can compromise the application’s security. This includes libraries, frameworks, and other software modules.

7. **Identification and Authentication Failures**  
   Previously known as Broken Authentication, this refers to issues with session management, password management, and other authentication mechanisms.

8. **Software and Data Integrity Failures**  
   This category includes vulnerabilities related to integrity failures, such as insecure deserialization, which can lead to remote code execution.

9. **Security Logging and Monitoring Failures**  
   Inadequate logging and monitoring can delay the detection of breaches, giving attackers more time to cause harm.

10. **Server-Side Request Forgery (SSRF)**  
    This occurs when an application fetches a remote resource without validating the URL supplied by the user, potentially exposing internal systems to attacks.
