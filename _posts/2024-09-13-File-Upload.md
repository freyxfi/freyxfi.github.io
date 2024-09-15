---
title: "File upload vulnerabilities" 
date: 2024-09-15 01:00:00 +0800
categories: [100DaysOfHacking]
tags: [challenge, Tutorial, File Upload]
image:
  path: https://i.pinimg.com/originals/1b/7b/6e/1b7b6edb3d0e457631438b8ed3eb58f0.gif
---

### What are we doing ? 
1. Understand this bug ? 
2. How to exploit this ? 
3. What are the mistakes by the developers ? 
4. How to fix them ? 
5. Practice this on academy 
6. Go Wild 
7. Peace 

### Understand the File Upload Bug 

Here are the resources which have all the information for this. The first one is the OWASP File Upload Cheat Sheet, which gives an overview of this bug. Check it out from [here](https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html#introduction). 
So the OWASP guide gives us recommendations on how to secure a file upload, but first, what the heck is this? 

If I put it in my own words: if an attacker uploads some malicious code and then executes it from the website to do some nasty stuff afterwards, then this is what I call a **file upload vulnerability**. 

### How to exploit this? 
1. Find a website that allows you to upload files. 
2. Check what file types it allows you to upload. 
3. Upload your malicious code. 
4. Check the path of the file. 
   > **Note:** For the examples in this blog, I will provide all the PHP codes you will need to exploit this vulnerability.
5. Get a shell back or information disclosure by reading the files.

### Mistakes made by the developer 

So I am not a developer, and I have never made a website where I allow people to upload anything. But now, if I was (or maybe in the future I will be) a developer, I would still not have this option. Let’s suppose if there is a developer like **Mr. Dev**. He had only one task: to make a website where employees can upload their reports from the `/reports-upload` section. This is a new function for the company, and Mr. Dev learned this from YouTube and made it. At least it works. 

But what **Mr. Dev** didn’t learn is how to secure that function. This is where things get interesting for hackers like us. Things go well for a while—company receives the reports, and Mr. Dev is happy. Then one day, the website gets hacked, and there’s a message from the hacker saying, "You have been hacked." So they called the cybersecurity department, and they investigated the issue and found out that the problem was in the file upload function. This is where the hacker got into the servers and website. Now this has a significant impact on the company, as the hacker owns the assets of the company and has a shell on the machine too. The hacker does what blackhat hackers do: downloads all the data, then deletes it, leaves their mark everywhere, and crashes the system.

So, let’s talk about what went wrong here? 

---

### Practice Practice Practice 

Well, as today is Sunday, I have time to practice on some labs—web security labs. I really love platforms like PortSwigger Academy for providing the basics, especially when I don’t want to waste time hunting for real-world targets. And I don’t want to ruin my Sunday testing and running into a super secure site, spending 10 hours on it. So, I will be solving the 7 labs related to **file upload vulnerabilities**. I’m assuming I will solve all 7, but who knows? 

Here are the 7 labs: 
1. Remote code execution via web shell upload 
2. Web shell upload via Content-Type restriction bypass 
3. Web shell upload via path traversal 
4. Web shell upload via extension blacklist bypass 
5. Web shell upload via obfuscated file extension 
6. Remote code execution via polyglot web shell upload 
7. Web shell upload via race condition 

Names sound interesting, and I’ve already solved two of them with ease. The third one was a bit tricky due to **path traversal**. I initially tried `../../`, but it didn’t work. Then, I remembered to use URL encoding, and it did the trick. 

Right now, I am on the 4th lab. It deals with **blacklist bypass**. The site is blacklisting `.php`, so I tried using `.php1`, `.php3`, and other double extensions, as we do in CTFs. It worked, but I still had to bypass the **Content-Type** to get the file to execute as PHP. 

---

### Exploits

To retrieve the content:

```php
<?php echo file_get_contents('/home/carlos/secret'); ?>
```

This is the code we used in the lab. In the real world, use this:

```php
<?php echo file_get_contents('../../../../../../../etc/passwd'); ?>
```

This will be best for the proof of concept (POC).

Now, if you come from a CTF background, then almost every easy CTF has a file upload vulnerability. So what do we do? We always go for a web shell. Here's the exploit:

```php
<?php echo system($_GET['command']); ?>
```
The system command will execute any system command such as id, ls, etc., all your system commands. This is also used in valid POCs.

---


### How to fix them? 

As OffSec says, the goal is not only to break things but also to help companies protect their digital assets. So, how can we help?

1. First, as seen from above, blacklist can be bypassed. So, companies should use **whitelisting** instead of blacklisting. 
2. Change the filename internally. See Twitter—when you upload a profile picture, the filename will be something like `834jhifrnhif.jpg`. This is really good, even next-level security. 
3. Don’t have subfolders that attackers can use to store files while attempting **path traversal**. 

---

### Final thoughts 

So, this is all for today. I haven’t been writing much lately, but I will make it a regular habit. I spent a lot of time on my computer today—playing HTB and doing Python took most of my time. In the morning, I had some extra plans, but things didn’t go as planned. So, I guess I’ll be working at night too. But it’s okay—I’m used to it. 

File upload vulnerabilities are very interesting. Even though the labs talked about them, hackers can also upload XSS payloads in images or other file formats. If you search GitHub, you will find payloads and ways to create XSS in `.pdf`, `.jpg`, and other extensions as well. 

With this in mind, I’ll end it here and talk to you all again next Sunday. I wish you all a great upcoming week—have fun! On top of that, my friend is calling me like crazy because he’s stuck in a CTF, so I have to go now.

---

My Twitter: [@wearehackerone](https://x.com/wearehackerone)  
Discord: xfi1337

