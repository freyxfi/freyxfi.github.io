---
title: "Week #4: Restart!!! Remember the Goal"
date: 2025-02-02 21:19:00 +0800
categories: [Web Security]
tags: [Web Security, CTF, Exam, Pentesting]
image:
  path: https://i.pinimg.com/originals/c8/08/91/c80891d61e16b4490ce940d4c7c6d660.gif
---

# What Happened Last Week?

- My company had a very important exam that lasted for 3 days, and it was crazy.
- Told my friends how easy it is to host a website on the dark web.
- Somehow, my tweets blew up when I yapped a lot.
- Stopped using Twitter excessively and set a timer.
- Learned new skills.
- Won a giveaway and got HTB VIP+.
- Started the TJ Null list for OSCP.
- Completed the HTB OWASP Top 10 track.
- Removed my WSL and reinstalled it.
- I kinda lost sight of my goal, so I will push myself harder now.
- Made new friends.
- Working on new projects.
- Using Microsoft Tasks to create a list of tasks.

# The Pentest Exam

If you’ve noticed, I’ve been kinda low-key for 3-4 days on Twitter. Usually, I’m very active and tweet a lot, so this means something’s up, right? My company had an important exam that’s crucial for validation. It’s a pentesting exam that runs for 2 weeks. The first week is all about testing, and the pentest itself goes on for 3 days. There are 2 machines: one is Linux, and the other is web-based. Sometimes, the Linux machine changes to Windows, but this time, we had one Linux and one web machine. I was assigned to handle the web machine, though I could have taken the Linux one as well. However, the company already had people handling that.

There were lots of meetings and planning, and it really worked out. I read a web report that helped me a lot—it had 200+ findings. Here’s what I did when the exam started: we found RXX, stored XSS, and IDOR. On the same day, we discovered the admin dashboard! I was told not to do FUZZ, so I ignored OTP brute force. Somehow, I changed my email to `admin@company.com`, but even though I got that, I couldn’t see the dashboard. The funny part is that I took over the admin email. Someone from the team told me that if you’re admin, you should be able to see what the admin sees. I was like, "No, I can’t," so there must be another way! After some grinding, we found out that the OTP bypass was all good. The `/otp/v3/xxx` endpoint had a rate limit, but `/otp/v1/xxx` didn’t, so we went with that, and the admin dashboard appeared. Easy takeover!

But that’s not enough—we needed RCE! While running `nmap`, I noticed something was up: Tomcat was running! From the file upload, we found a particular point, uploaded a file, grabbed the web shell, and then got a bind shell. Win-win! But we didn’t stop there. We found out that if we could change the configuration file of the users in Tomcat, we could add ourselves. That was so cool! It wasn’t that difficult, but the Linux machine was way cooler. None of the exploits worked, and only the LDAP port was interesting.

# Host Your Own .onion Site

Well, let’s make this really short. DM me on Discord, and I’ll show you how easy it is to host a site on the dark web! I can make a video about it, but God, I need a mic, lol. I had one person’s tweet bookmarked, and I promised them to make a video. Maybe they thought I forgot about it.

# Is Twitter a Problem?

No, it’s not. I joined Twitter to keep an eye on the infosec community, but now everyone is yapping, and my timeline feed has turned into arguments of people fighting with each other. So, I’m keeping my distance.

# Learning Something New

I have a list of things I want to cover, and I will now. I really want to wake up early and be low-key.

# I Won a Giveaway for the First Time

I got an HTB VIP+ subscription, and I’m really loving it. I still can’t believe I won it, but I have an idea how, lol. I know what the guy thought when he put me there!

![research](https://pbs.twimg.com/media/GipbHQJWcAEmAu1?format=jpg&name=medium)

# Holy Cow, I Completed My First HackTheBox Track: OWASP Top 10

Well, yeah, that makes sense. I never had any subscription before, so I just played the active machines, and that’s it. But now, I have my eyes on some cool tracks. For example, the Active Directory 101 is the next target, followed by some hard ones too. I just want to improve my skills and keep grinding. Maybe I can complete the TJ Null list, but I need discipline and proper timing in my daily schedule.

![research](https://pbs.twimg.com/media/GitJcPGXsAAn2th?format=jpg&name=medium)

# My Lovely WSL Got Removed

I removed my WSL—not accidentally—and then reinstalled it. It’s like 5 minutes of work, but I lost all my toolkits and sources. But who cares, brother? We can install them again, hahaha.

# HTB and CPTS

For this month, I’m all set for HackTheBox, Active Directory, and CBBH. I’ll make sure to keep my mind on track and enjoy the process. I need a good note-taking method. If you have any, please say hi to me on Discord.

I think that’s it. I’m in the middle of a machine called "Forest" from HTB. It seems like a good starting point for Active Directory attacks.

# Goals for Next Week

- Complete HTB Active Directory 101.
- Finish CBBH up to Module 6.
- Read 100 reports.
- Read 100 good write-ups.
- Hack for 4 hours daily (excluding learning or doing HTB).
- MMA hardcore—learn new skills, be strong, but stay humble.
- Do 30 Spanish lessons!

This all starts on Monday, and for this, I have to wake up at 4 AM, which means I have to sleep early.