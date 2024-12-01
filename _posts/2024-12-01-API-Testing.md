---
title: "API Testing and The Last Month"
date: 2024-12-01 01:00:00 +0800
categories: [Web Attacks]
tags: [Challenge, Tutorial, API Testing]
image:
  path: https://i.pinimg.com/originals/f8/bd/89/f8bd898260e3919ee974bcb2bb42f4dc.gif
---

## Topics We'll Cover
1. **This Week Wrap-up**  
2. **Introduction/Why Do API Testing?**  
3. **Key Concepts**  
4. **Tools and Technologies**  
5. **API Labs**  
6. **What to Test**  
7. **Real-Life Example**  
8. **Conclusion**

---

# This Week Wrap-up 
I plan to write short yet effective blogs to share ideas and keep track of my progress while helping others do the same. It's about staying disciplined, which is why I’m committed to weekly blogs.  

Today is December 1, 2024—another year is passing by. I'm a bit unsure whether to call it successful, as there’s so much still to achieve. However, looking back at what I’ve done until November, I’m proud of my progress, both physically and mentally.  

This week was special. I completed all my Russian lessons, organized an inter-university CTF with my company, and for the first time, helped run a CTF instead of just playing. It was an amazing experience! I met new people, exchanged contacts, and networked—something very out of my comfort zone.  

The CTF competition my company hosted was fascinating. It highlighted how our organization has two distinct branches: one for breaking and hacking and the other for teaching. For the past five weeks, I’ve been working with DefHawk and CRAC, focusing on learning about recent CVEs, APT29, and red-teaming tools.  

This month, I plan to deep-dive into Windows and Active Directory (AD). I'll explore AD components in-depth and might even set up a forest! Expect upcoming posts to delve into this, possibly including related Hack The Box (HTB) machines.

---

# API Testing 

API testing is a vast and crucial topic in the realm of testing. Trust me, it often uncovers the hidden and critical vulnerabilities companies least expect. For instance, a hack I performed three months ago led to financial PII leaks by exploiting an exposed API endpoint.  

In this post, we’ll discuss scenarios and strategies related to API testing.

### Starting Point
The first thing to do in API testing is **recon, recon, and more recon** to gather the documentation.  

Personally, I don’t immediately jump into API testing on a target. Instead, I observe whether APIs are involved when I make changes, such as requesting or updating something. I then take note of this interaction.  

You might be wondering what are API documents? Think of any service you’ve used, like a manga or anime site, or creating a Discord/Telegram bot. They often provide a set of rules for interacting with their APIs: tasks you can perform, features you can add, or data you can manipulate.  

For example:
- **NASA**: [https://api.nasa.gov/](https://api.nasa.gov/)  
- **Pinterest**: [https://developers.pinterest.com/docs/api/v5/introduction/](https://developers.pinterest.com/docs/api/v5/introduction/)  

The Pinterest example clearly showcases how API documentation looks. It lists the operations you can perform with API keys.

**Note:** Not all operations and APIs are listed in the documentation. There are often unused APIs and hidden actions that you’ll need to discover.  

When conducting recon, ensure you carefully study API docs and watch for these hidden aspects. If I may I would Like to gives these paths. Non of them are hidden path just common ones which Companies uses so feel free to check or update your wordlist. 

```
REST API Documentation Paths

    /api-docs
    /docs
    /swagger
    /swagger-ui
    /openapi
    /api-explorer
    /documentation
    /help
    /api/v1/docs
    /api/swagger.json
    /api/openapi.json
    /api/swagger-ui.html
    /v1/docs
    /api/v2/docs
    /swagger.yaml
    /openapi.yaml
    /api.json
    /openapi.json
    /api/v3/docs
    /developer/api-docs

API Developer Portals

    /developers
    /developer
    /api/developer
    /developer/docs
    /api/developers
    /api/guide
    /dev/api-docs
    /developer-guide
    /api/v1/reference
    /reference

GraphQL API Documentation Paths

    /graphql
    /api/graphql
    /graphql-docs
    /graphiql
    /playground
    /graphql-explorer
    /v1/graphql
    /api/v2/graphql
    /graphql/schema
    /graphql/docs

Alternative API Documentation Paths

    /redoc
    /api/redoc
    /redoc-ui
    /apidocs
    /api-help
    /api/manual
    /rest-api-docs
    /developer/documentation
    /explorer
    /api/ui
```

I have more tips, but honestly, you should just download this: [API Wordlist by Chris Lockard](https://github.com/chrislockard/api_wordlist). It’s incredibly helpful. Also, don’t forget to check out **Assetnote Wordlists** for additional resources.  

Now that we’ve covered wordlists and recon, what’s next?  

---

## Finding Hidden Endpoints and Parameters

The recon process doesn’t end here—it evolves as we move forward. At this stage, we become more **interactive** with our targets.  

### JavaScript Files: A Hidden Treasure  
You’ll be amazed to discover that JavaScript (JS) files often contain a wealth of information—and sometimes pure gold. These files can reveal hidden API endpoints that might lead to critical vulnerabilities. For instance, you might uncover financial endpoints or APIs leaking PII (Personally Identifiable Information).  

I personally love using the **Link Finder** extension on Burp Suite to extract URLs from JS files. I save the output as logs and carefully analyze them. This process can be time-consuming, and yes, sometimes I come up empty-handed, but the effort is always worth it.  

---

## Interacting with the API

Once you’ve uncovered hidden endpoints (though not all, as there are always more to find), the next step is to interact with the API. The goal here is to understand its functionality and behavior.

### Steps to Interact with APIs:
1. Open Burp Suite and start making requests to all identified endpoints.
2. Test their responses and behaviors.  
3. Use the `/OPTIONS` HTTP method extensively—it helps identify supported methods and reveals what the endpoint can do.  

**Tip:** Use Burp's proxy history to explore API points and uncover additional information.  

---

## What Can You Do with APIs?  

Here are some common actions you can test against APIs:  
1. **Update any user**  
2. **Delete any user**  
3. **Post data**  
4. **Price manipulation**  
5. **Bulk changes**  
6. **Crash the API** (e.g., checking rate limits)  
7. **Account takeover**  
8. **PII leaks**  
9. **And much more...**

---

### Adjusting Content Types  

Sometimes, APIs require specific content types for their requests to process correctly. Common formats include `JSON` and `XML`.  

As you begin interacting with the API, you’ll get a sense of what it expects. Until then, **hit-and-trial** is your best friend. Keep testing different content types and parameters to uncover vulnerabilities.  

---

API testing is a journey of persistence and exploration. Stay curious and keep digging!
 

---
I fell asleep midway after mentioning that I was writing a blog on API testing. Just woke up—sorry about that! Usually, I write blogs on Saturdays and upload them on Sundays, but today’s a bit different.  

I wanted to work on Active Directory (AD), but I’m lacking the RAM to set things up properly. Instead, I’ll check if **Hack The Box (HTB)** has something exciting to offer.  

---

## Mass Assignment or Auto-Binding in API Testing  

One of the most interesting aspects of API testing is **auto-binding** or **mass assignment**. I recall watching a talk at DefCon about it, where the speaker demonstrated a scenario where an application revealed additional options in its `/GET` response. These parameters could then be used in `/POST` requests to manipulate the application’s behavior.  

If you're interested in trying this out, there's a lab on **PortSwigger Academy** about it. You could also find similar labs elsewhere with some digging.  

I’m a bit too lazy to fire up the lab and add screenshots here, but here’s how it works:

### Example Parameters in `/GET` Response  
When inspecting `/GET` responses, you might come across parameters like:  
1. `price`  
2. `update`  
3. `xx_v-update`  
4. `discount`  
5. `delete-file`  
6. `company-sec`  
7. `bd_allows`  
8. `is_Admin`  

(*Note: These are just random examples I came up with.*)  

---

### How to Exploit These Parameters  
1. Open **Burp Suite Repeater**.  
2. Make a `/POST` request to the same endpoint.  
3. Use the discovered parameters to manipulate the application’s behavior.  

The idea is to test these parameters to "break the logic" of the application. Manipulating these can lead to vulnerabilities like unauthorized access, data manipulation, or privilege escalation. Once you get the hang of it, it becomes both fun and rewarding!  

---

## Server-Side Parameter Pollution (SSPP)  

I wasn’t planning to talk about this, but hey, let’s cover it anyway. **Server-Side Parameter Pollution** occurs when an application does not properly handle multiple identical parameters in a single request. This can lead to unpredictable behavior or even bypass certain security mechanisms.  

We’ll dive deeper into SSPP in upcoming posts. Until then, keep exploring!


# Server-Side Parameter Pollution (SSPP)

If you ask an older hacker, they might respond with, "Are you talking about HTTP Parameter Pollution?" That’s the reaction I get all the time. And yes, SSPP is essentially a form of **HTTP Parameter Pollution** (HPP).  

Many cool hackers on Twitter share amazing tricks and blogs on this topic—how they dig deep, discover internal APIs, and manipulate them to achieve their goals. As always, this involves staying persistent with reconnaissance to uncover hidden internal API points.  

---

## Key Note: Hidden Points Aren’t Bugs  
Finding hidden points isn’t considered a bug. **It’s all about the impact** what you can do with those points afterward.  

---

## SSPP Testing Checklist  

1. **Identify the Testing Point:**  
   Pinpoint where SSPP could occur, such as endpoints with multiple parameters.  

2. **Start Making Requests:**  
   Look for error messages returned by the server. These are clues to crafting your payloads.  

3. **Understand the Error Responses:**  
   Study the server’s responses to differentiate between valid and invalid parameters. This can help in parameter manipulation.  

4. **Use Encoding Tricks:**  
   Inject payloads with encoded characters like `%26`, `%23`, etc., to bypass server-side checks or truncate requests. *(It's been a while since I used this; I need to practice more!)*  

5. **Inject Invalid Parameters:**  
   Sometimes invalid parameters will trigger error messages that reveal the correct ones. For example, the server might say, “Oh no, this is wrong! Use this instead.”  

6. **Exploit the Parameters:**  
   Once you have the correct fields, use them to access internal APIs, update sensitive information, or expose unintended data.  

---

### Final Note on API Testing  
When testing APIs, **keeping detailed records is crucial**:  
- Document all endpoints and parameter fields used.  
- Differentiate between public and private endpoints.  

Also, remember that **JS files are your friends**:  
- Read JavaScript files to understand the application's flow.  
- If internal JS files aren’t accessible, rely on your logic and reconnaissance to uncover more.

JS files often contain hidden treasures that can lead to internal exposure or vulnerabilities.

---

## Personal Goals for the Week  

- **More hacking.**  
- Active Directory deep dive.  
- Complete **Russian Unit 8**.  
- Wrap up **APT29** analysis.  
- Solve 5 CTFs.  
- Watch missed talks from **DefCon 32**.  
- Engage in 2 bug bounty programs.  
- Start a 30-day streak of **500 pushups per day**! 💪  
- Play API challenges.  
- Study **web cache deception** (next blog topic).  
- Learn 5 new things and share them.  

---

### Upcoming Challenge: TryHackMe’s Advent of Cyber 2024  
I’m excited to join **TryHackMe’s Advent of Cyber 2024**, even though I’m sure I won’t win a prize I’m not the lucky type! But it’s all good. Participating will at least help me keep a streak going and improve my skills.

---

Let’s keep hacking and learning! 🚀
