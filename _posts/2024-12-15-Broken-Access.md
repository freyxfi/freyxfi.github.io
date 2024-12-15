---
title: "Broken Access Control & What happen this week"
date: 2024-12-15 19:00:00 +0800
categories: [Broken Access Control]
tags: [Tutorial, Web-Security, BAC]
image:
  path: https://i.pinimg.com/originals/0a/f5/9f/0af59f26773f98c2c29352c11f9d09b6.gif
---

# What happen this week?

Well hello everyone! This week was totally crazy—up and down—and quite slow too, but I did a lot of things. Let's mention them here. If you are reading these weekly blogs, you are already familiar with how we do this. In each blog, we discuss our weekend work and then talk about one topic which we find interesting! If you are here just to look for the access control topic, I will suggest you skip the weekend part and jump to it right away. But then you will miss out on a connection between you and me, haha.

# Here are the things I did this week

1. **Made pentest report for the company**  
   I have good experience in making long pentest reports and how the structure is meant for industry standards. I feel confident in working with long pentest reports of 100-200 pages! Sorry to say bug hunters, all those informative things you got can work in pentest too, lol.

2. **Worked as a team in the pentest—haha, was quite good**  
   We have a Discord channel for teamwork, and I think I started feeling good with the team. I have been a solo hacker for long, and I still feel I do much more when I am alone instead of with a team. But team and collaboration are also keys to success. That's why I am working on my connections too, and in the long term, it will help a lot. There is no trick to making connections—just be a good human and kind, and that's it. I think that's how it works. And yeah, be real, which is so rare.

3. **Focused on AD—got IPv6 Attack in my pocket**  
   I barely got time for AD attacks, but I took some time to look into IPv6 attacks. We will talk about this as this is a real deal, and this will work in real-world testing. I don't think this is that much old—this is all about MitM6.

4. **Same going with Russian lessons**  
   Well, I am on Unit 9. I haven't completed the unit, but this one is all about the bus and stop names, so this is easy, haha. Right now, when I am writing this, I was trying to figure out how to say 'dog' in Russian and I got it. I think learning new languages also sharpens your brain.

5. **Got a haircut**  
   Yes, I cut my soo soo long hair as now 2025 is coming soon, and I will be fighting again. So, I need to be in shape. One more thing: whenever I decide to be serious in life, I cut my hair shorter. Also, for MMA rules in our dojo, we cut hair to the minimum length so other fighters can't grab it while grappling.

6. **Major update: shifted home**  
   Well, this is really the major update. We have shifted to a bigger home than the previous one, and now I am back in a colony. It means I can't do boxing and training whenever I want. Now I am thinking about what to do with my mountain bike.

7. **Then I got sick, lol, and recovered in 2 days**  
   I also got sick because of the ice bath I took, lol. I know this is so stupid doing this in the month of December, but I think it didn't affect me that much. What happened afterwards is I mostly hung here and there in shorts, lol, so maybe that's the thing.

8. **My previous bug is still in blocker stage**  
   The bug is still in the process, and the triager put the blocker on the customer, haha—that's so nice.

9. **Got my mind on cache deception—completed all PortSwigger labs on it**  
   I found a very interesting topic which caught my mind. I was always so into cache and how this works since the time when I started studying networking, and this curiosity will drive more in upcoming events.

10. **Playing Shadow Fight 3 now**  
    I totally needed a mobile game, so I downloaded Shadow Fight 3 and am playing it now. It's Day 5 and I am on Level 3, but hey, that's really interesting.

11. **Took lead in company meet session**  
    I have to make a presentation for a topic to present, so I chose **Broken Access Control (BAC)** for it. I will be delivering it on the 18th, so after writing this blog, I will make a presentation on Canva. Let's see—I suck with PPTs.

---

# Broken Access Control

Wow, so we are starting with the main topic finally! After covering the weekend talk, we are here. To understand it better, let's split this into topics. We will talk about:

1. What is BAC?  
2. Why it is critical  
3. Can we please talk about real world?  
4. Importance of Access Control  
5. How BAC happens  
6. Example of BAC vulnerabilities  
7. Testing for BAC  
8. Do we need tools?  
9. Mitigation techniques  
10. Real-world cases  
11. Last words

Wow, so there are lots of things to discuss today. As you know, BAC is really vast. And sorry if I am mentioning BAC instead of **Broken Access Control** again—it's just fast to type, haha.

# Broken Access Control

Wow, so we are starting with the main topic finally! After covering the weekend talk, we are here. To understand it better, let's split this into topics. We will talk about:

1. What is BAC?  
2. Why it is critical  
3. Can we please talk about the real world?  
4. Importance of AC  
5. How BAC Happens  
6. Examples of BAC Vulnerabilities  
7. Testing for BAC  
8. Do we need tools?  
9. Mitigation Techniques  
10. Real World Cases  
11. Last words  

Wow, so there are lots of things to discuss today. As you know, BAC is really vast. And sorry if I keep mentioning BAC instead of *Broken Access Control* — it's just faster to type, haha.  

---

## 1. What is BAC?  

Broken Access Control is a security issue that occurs when users can access data or perform actions beyond their permissions. To explain it simply: you can do things that the application doesn't allow you to do.  

Think of it like this: I tell you that you can't get out of the house, and I lock the door. But you get out through the window! Wow, that's how you break access for your own means. Similarly, in BAC, you have predefined access, but you are able to bypass it.  

One more thing — we are focusing on *Broken Access Control*, but we are **not** talking about *authentication bugs* here. That is a separate topic for another blog.  

---

## 2. Why is it critical?  

Have you noticed that people often say "Go hunting for BAC"? You may have seen big hackers advising: "Just look for BAC, and it will give you your first bug." And that's true.  

All you need to do is understand the application or program and find ways to bypass what it doesn't allow you to do. If you DM me, I can show you my reports — they are *so interesting*!  

But why is it critical? Let's look at the **OWASP Top 10**:  
[https://owasp.org/Top10/](https://owasp.org/Top10/)  

Do you see it? BAC jumped from the **fifth place** to **number 1**. We are talking about critical severity here. After this, I recommend reading the detailed OWASP description:  
[https://owasp.org/Top10/A01_2021-Broken_Access_Control/](https://owasp.org/Top10/A01_2021-Broken_Access_Control/)  

This will make a lot of sense.  

---

## 3. Can we talk about the real world?  

I know you want to know the impact of BAC in the real world. How do you find it? What do you look for? I also had these same questions when I started. So, I’ll include findings from my friend Ayush and me to give you a taste of BAC in real-world scenarios.  

**Ayush's Bug:**  
A targeted company had a buy/sell feature where users had to wait **72 hours** before selling an item. Ayush thought, *"Why wait 72 hours?"* So he started looking for JavaScript files and found a variable: `sell_validity`. He modified it, bypassed the restriction, and sold/bought the item immediately. Time and protection destroyed — BAC wins!  

**My Bug:**  
In a targeted company, I found an issue with the payment receipt. I went to the application, and it led me to the **subscription page**. I started looking for hidden URLs and used Wayback Machine to find some old links.  

I discovered a URL: `payment_success?id=xxx` under the payment directory. I used Burp Suite Intruder with `id=xxx` as payload and successfully retrieved payment receipts with PII leaks. Increasing severity was key here.  

BAC is all about breaking things!  

---

## 4. Importance of Access Control  

Think about this: I am using an application that secures my data, and I am paying for it. For example, if I pay for **Twitter Blue**, I expect to enjoy the features. But imagine a hacker friend also enjoying those same features for free by breaking access control layers.  

BAC has many bugs, such as:  

- CWE-22: Improper Limitation of a Pathname to a Restricted Directory  
- Path Traversal: `.../...//`  
- Improper Link Resolution Before File Access  
- Exposure of Sensitive Information to Unauthorized Actors  
- Incorrect Default Permissions  
- Improper Authorization  
- Cross-Site Request Forgery (CSRF)  
- Forced Browsing  
- Open Redirect  
- Missing Authorization  
- Vertical/Horizontal Privilege Escalation  

This list is **copied from OWASP** so I’m sure you are familiar with most of them. We’ll talk about each of these separately in future blogs.  

---

## 5. How does BAC happen?  

So how does *Broken Access Control* actually happen? Are developers stupid?  

Well, no. I wouldn’t say that. But sometimes developers make mistakes, especially with misconfigurations and permissions.  

- **Poorly implemented RBAC (Role-Based Access Control):** Developers fail to restrict roles properly.  
- **Predictable URLs:** Sometimes, lucky guesses can lead you to sensitive admin pages or actions.  

Example:  
Imagine I own `frey.com` with an admin panel at `frey.com/admin`. If you access this, it asks for credentials. But what if you find a URL like:  
`frey.com/admin/deleteuser.html`?  

Clicking that could let you delete any user. Boom! BAC exploit.  

---

## 6. Examples of BAC Vulnerabilities  

Here are the three kings of BAC:  

1. **IDOR (Insecure Direct Object Reference):**  
   If you follow that guy with the smirking emoji brand watch (haha, Z-wink), you already know IDORs. Just enumerate IDs like `1234`, `1235`, `1236`, and find sensitive data.  

2. **Horizontal Privilege Escalation:**  
   Access or modify data of users on the same level as you. Think of it as *"staying horizontal."*  

3. **Vertical Privilege Escalation:**  
   Access data or perform actions beyond your role, like a normal user deleting an admin account.  

---

## 7. Testing for BAC  

When testing for BAC:  

1. Open your target application.  
2. Click **everywhere**. Test **every feature**.  
3. Note what you can and can’t do.  
4. Perform **role manipulation**.  
5. Use fuzzing techniques to explore boundaries.  

---

## 8. Do we need tools?  

Yes! While you can hack with just browser DevTools, having **Burp Suite** makes life much easier.  

Professionals use other tools too, but Burp Suite is enough to start. Just don’t download cracked versions unless you like malware, haha.  

---

## 9. Mitigation Techniques  

For developers:  

- Enforce **least privilege** principles.  
- Use **server-side checks** for sensitive operations.  
- Implement strong **RBAC**.  
- Conduct regular **access control audits** and testing.  

---

## 10. Real World Cases  

If you want real examples, search HackerOne reports using this dork:  site:hackerone.com intext:"Broken access control"

The first result will probably be an article on how to find BAC.  

---

## 11. Last words  

Oh, I almost forgot — I hit **3K followers**! Thanks a lot for that. I’m still crazy and dreaming of fighting in the UFC one day (as long as I don’t get injured).  

For BAC: **Keep breaking things!**  

Thanks for reading. One last question:  
**How many of you pray daily?**  
