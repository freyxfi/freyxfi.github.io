---
title: "Week #2 Starting with SQLi !  "
date: 2025-01-12 22:19:00 +0800
categories: [Web Security]
tags: [Web Security, SQLi]
image:
  path: https://i.pinimg.com/originals/ca/7d/57/ca7d5760efa1edd4308ad0ec5fbe1fdc.gif
---

# What I Did This Week?

1. Exploring New Active Directory CVEs
2. Practicing more Active Directory
3. HackTheBox Season 7
4. SQL Injection has been started
5. MMA hitting me hard
6. Got another screen!
7. Working on confidential projects
8. Rust Programming
9. Making connections

# Exploring New Active Directory CVEs

This is kind of heartbreaking that I found some cool CVEs published by SafeBreach. Yes, I am talking about LDAPNightmare. There are actually two CVEs related to that, which Yuki Chen exploited: CVE-2024-49112 and CVE-2024-49113. One is RCE, and another one is quite interesting, as it can crash the system. The exploit is way interesting; when I tried reproducing it, I successfully failed at the last step because there is some domain I have to register for it to work. However, I think if I can make it run locally, I can modify the /etc/hosts file and see how it works, or just use the SafeBreach registered domain used in the POC. You can read the whole article here: [SafeBreach Blog](https://www.safebreach.com/blog/ldapnightmare-safebreach-labs-publishes-first-proof-of-concept-exploit-for-cve-2024-49113/).

# Practicing More Active Directory

Am I practicing AD regularly? Well, to be honest, I am not. I need to subscribe to HackTheBox and complete the Active Directory 101 path, but I am waiting for my friend to pull off the CPTS voucher for me. Then, I will have lab + machine access, and we will do hardcore hacking.

# HackTheBox Season 7

Oh yes, I am playing HTB Season 7 as this is free, and your bro is broke ass! So yes, I will use this to solve some boxes, and maybe I will make some rough write-ups if needed. However, I am not very excited, as now it does not feel as cool as it used to be a year ago! Back then, it felt like something I was really doing.

# SQL Injection Has Been Started

Dude, what should I say? Finding SQLi manually is very time-consuming! In BB programs, it's like diving deep into hell. My SQLi methodology was quite simple: just put `'` or `"` and see if something happens, then proceed. I used to do this after mapping the application as much as I could, then see it. But it's way more than that! I have promised that I will make a full SQLi methodology after this week, but please give me time. I will make it another article, not just a weekly blog titled SQLi, as I am going through all the methods. There are some wonderful articles and reports I have seen, which are really out of the box. I solved some PortSwigger labs, which are cool. This makes me wonder: should I approach targets with some dorks?

# MMA Hitting Me Hard

Oh boy, I got lots of injuries this week—on my neck, my wrist got injured, I got an elbow hit just above my eye, my fingers got injured badly, and there's a lot of pain in my body. It's cold, and I am doing this, but the grind never stops. I do crazy hard workouts. Can you believe I take on 90kg? I am in the featherweight division, but I feel there is way more practice needed. I will register for nationals!

# Got Another Screen!

LOL, I just got an HDMI to VGA adapter, and now it's way better!

# Rust and Connections

I am feeling very tired, but I have to work on some projects because today is Sunday, and then Monday = office. There are some pending projects I have to finish overnight or at least get 70% done. By the way, what does a good OSINT CTF look like? Have you ever wondered? I am still working with Rust, made that guessing game with random numbers saved my ass! Also, my Discord username has been changed; please send me a friend request on @noplacetochat. I have joined some good Spanish learning servers too, so adios, guys :)

# For Next Week

1. Finish SQLi, make my own methodology
2. Make a YouTube video about it
3. xxxxxx on xxxxxxxx
4. Share a good technique on the internet
5. Read the pending PDFs
6. Read 50 write-ups
7. Read 100 reports
8. Pray
9. There are some things I can't remember, but I have to do them
