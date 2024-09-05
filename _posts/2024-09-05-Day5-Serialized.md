---
title: "Day 5 of 100 Days Of Hacking" 
date: 2024-09-06 01:00:00 +0800
categories: [100DaysOfHacking]
tags: [challenge, Tutorial, Insecure Deserialization]
image:
  path: https://miro.medium.com/v2/resize:fit:1400/0*zO2LGJNcKBF6LAfx.png
---

### What happened today?
1. Completed my B.Tech
2. Python Programming
3. Insecure Deserialization
4. Taught things to my friend
5. Hacked two targets and failed
6. Working on my report

### Completed My B.Tech Degree 

Hello, and welcome back to another day of hacking! I'm your cool hacker friend Frey, and today I’ve got some exciting news: I finally completed my B.Tech (Bachelor of Technology) in Computer Science. It was a wild ride! Although most of my knowledge came from the internet, books, and blogs, I can't deny that college gave me some good memories. Now that chapter is over, and I’m off on a new adventure. More on that in another blog! But for now, let’s dive into today’s bug type and what I did.

### Insecure Deserialization 

If you remember, on Day 3, I started exploring Insecure Deserialization but got sidetracked with Google Dorking. So today, I decided to revisit the topic. Whenever I want to study something, I deep dive into research—searching websites, watching videos, and making my own notes. I believe this is the best way to learn in today’s world, as everyone has their unique perspective.

#### What is Insecure Deserialization?

To understand this, we first need to know what serialization and deserialization are.

- **Serialization**: The process of converting data into a series of bytes.
- **Deserialization**: The process of converting those bytes back to their original state.

To simplify this for a 9-year-old: think of ice cream. In its original state, it’s unpacked. Then it's wrapped up at the factory. When you get home, you unwrap it, returning it to its original form. Similarly, serialization wraps data, and deserialization unwraps it.

#### What’s the issue?

The danger lies in how data is processed during serialization. Attackers can inject malicious code into serialized data. This can lead to major security risks like:
- **RCE (Remote Code Execution)**: Injecting code that can be executed on the server.
- **Information Disclosure**: Gaining access to sensitive data.
- **Access Control Issues**: Modifying values (e.g., from `0` to `1`) to gain unauthorized admin access.

I plan to dive deeper into this topic with examples and code in future blogs, so stay tuned!

### Taught Things to My Friend 

Today’s blog is shorter because I spent most of the day teaching a friend how to hack. We spent six hours hacking together! I showed him how to identify access control vulnerabilities, do some recon, and review code. We dug deep into an application and found some cool stuff. It was like a flashback to my CTF days in college, but this time I was the mentor.

### Hacked Two Targets and Failed 

This part is interesting. My friend and I targeted two sites but didn’t succeed. I did find something, but I don’t report until I can make a big impact. It’s not about rushing for me—it’s about learning and enjoying the process.

We were using Kali Linux on my friend's laptop, but I ended up spending an hour downloading and configuring the tools for him. He was confused about what to do, mainly because of the overwhelming advice from people online. A lesson here: not all advice applies to everyone!

Oh, and I almost forgot—I still need to enroll in a certification course today. Gotta go! See you tomorrow.
