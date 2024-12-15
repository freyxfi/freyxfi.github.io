---
title: "Active Directory Setup And More"
date: 2024-12-06 01:00:00 +0800
categories: [Active-Directory]
tags: [Tutorial, Active-Directory]
image:
  path: https://i.pinimg.com/originals/fc/9e/a9/fc9ea9b1e2b3191efcfec856e4073fb2.gif
---

# Weekly Report

Before starting, I want to apologize that this post isn't about GraphQL as I initially planned. I'll cover that topic after going through the famous server-side bugs on my list. So, maybe the next post will be about Broken Access Control or something similar.

Hello everyone, I'm back with another weekly blog. Let me first share what I worked on this week. I'm not the smartest or most talented person, but I strive to improve every day. Here's what I accomplished this week:

---

## 1. Active Directory Setup

As I mentioned in [this tweet](https://x.com/Freyxfi/status/1862834655256256617), I focused on Active Directory (AD) this week. I created a local lab setup for practice, which used up all the space on my computer (not great, but worth it). Here's a quick guide to help you set up your own AD lab:

### Requirements:
- 1 server as a **Domain Controller**  
- 2 Windows machines  
- 1 attacking machine (e.g., Kali Linux)  

I’m also working on an AD repository for GitHub, which will include detailed steps. It's private for now, but I'll make it public soon.

### Setup Steps:
1. Download Windows Server 2019 from [here](https://www.microsoft.com/en-in/evalcenter/download-windows-server-2019).
2. Get an attacking machine: **[Kali Linux](https://www.kali.org/downloads/)**
3. Download two Windows 10 machines from [here](https://www.microsoft.com/en-in/evalcenter/download-windows-10-enterprise).

Once done, connect the computers to the server (Domain Controller) and create user accounts. I went with a **Stark Industries** theme, so expect some themed posts on my Twitter soon. Feel free to ask questions about this setup.

---

## 2. Learning AD Attacks

This week, I also learned and performed four AD attacks locally:
- **LLMNR & NBT-NS Poisoning**
- **SMB Relay**
- **AS-REP Roasting**
- **Kerberoasting**

These are beginner-friendly attacks, but there's a lot more to explore in AD. I used [Impacket scripts](https://github.com/fortra/impacket) and SMB services. AD is often described as "easy but vast," and I’m committed to diving deeper into it in December.

---

## 3. Bank Testing

This was an exciting part of my week. My office team is working on a banking application, and we found **20+ bugs in a single day**, including:
- **Admin takeover** (via a debug error exposing hidden paths and admin email)
- **User takeover** (via an easy IDOR vulnerability)

While the team expects me to uncover something more impactful, like an RCE, I’ve requested more time to crack it. Stay tuned—I’ll share more as it unfolds!

---

## 4. Business Logic Error Bug

I reported a bug to a major social media platform this week. While I can’t share details until they review it, it involves bypassing a restriction on creating shortcuts in a dashboard by manipulating index values. I’m curious about their bounty payout for this!

---

## 5. Completing Unit 8 in Russian

As mentioned in previous blogs, I’m learning Russian. This week, I completed **Unit 8**. While my Russian isn’t fluent, I can now hold basic conversations and have made several Russian hacker friends!

---

## 6. CTF - Hack The Box

Although I don’t play Hack The Box as much anymore, I solved two machines this week. They were relatively easy, but enjoyable nonetheless. I also participated in an API CTF, which felt like a code review challenge—it was really cool.

---

## 7. DEF CON 32

I watched the talk *“DEF CON 32 - Gotta Cache ‘em All: Bending the Rules of Web Cache Exploitation”* by Martin Doyhenard. It blew my mind! The depth of their research inspired me to dive deeper into web cache exploitation. Time to explore this area further!

---

## 8. Networking and Connections

This week, I connected with several amazing hackers. If you're reading this, feel free to message me or connect on Discord: **xfi1337**.

---

## 9. MMA Training

I focused on grappling this week instead of striking. My goal is to prepare for a fight in 2025. For now, I’m fixing my sleep schedule and building a disciplined training routine.

---

## Closing Thoughts

Thanks for reading! I’m not setting explicit goals here, but I plan to write about **Authentication** and **Broken Access Control** next week. Stay tuned!

---
