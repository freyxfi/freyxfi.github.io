---
title: "Day 1 of 100 Days Of Hacking" 
date: 2024-09-01 00:00:00 +0800
categories: [100DaysofHacking]
tags: [challenge, Tutorial, Race-Condition]
image:
  path: https://shared.akamai.steamstatic.com/store_item_assets/steam/apps/1209950/header.jpg?t=1673514123
---

### Intro

I don’t want to write a lot of off-topic things here, as I don’t want to end up in OSINT, lol. So, let’s keep it clear and cool. By the way, happy new month to all of you! Let’s get that energy and start.

### Things to Do Today

I’m not planning to do a lot today since it’s Day 1. I’ll start with some small tasks. I already listened to the Critical Thinking Episode 1, which was good, and I could go and find the recording right now. But hey, I want to keep this going and give it my all. So, here’s the plan: I’ll focus on a web bug type today. Let’s choose Race Condition (CWE-362) and dive into it. I know a little bit about it, but I want to learn more. Give me 30 minutes, and I’ll come back and share what I’ve learned since this is a real-time blog. Yeah, I’m using this blog as my notes—funny, right?

### Oh Wow, I’m Back—Done with Race Condition (Theory)

![race condition](https://vickieli.dev/assets/images/hacking-01.png)

I’ve gathered resources and read through them. It took me an hour, but I must say, race conditions are awesome, especially if you’re hacking something like a voting system. I can’t believe I already knew about this! Do you all remember studying multiprocessing and multithreading in your OS class? Well, that’s it—this is all based on that. By the way, you know about that deadlock thing we studied? Let’s talk a little about race conditions.

I’ll write a full detailed post on this later, but for now, let’s see how it happens. The cause is in thread processes running simultaneously, where one thread’s result depends on another thread. In short, it’s all about timing and luck. If you have these two factors, you’ve got a race condition. If you want to play with it, try solving "Skyfall" on HTB. Now, I’m thinking about what to do next—let’s do some LeetCode.

### LeetCode

Don’t judge me; I’m just doing it to look cool like those devs on Twitter. Well, I just want to use my brain, so let’s see what the problem is today.

(2022. Convert 1D Array Into 2D Array) This is an easy problem. Let’s see—so we’re given a 1D array, and we have to convert it into a 2D array. Alright, this means if we have `original = [1, 2, 3, 4]`, it should become a 2D array with an up and down structure. Oh no, now there’s that time complexity to consider. I forgot all my DSA, but it’s easy since it’s based on iteration, and I can loop to make it 2D. Let’s look at the sample case.

![pic](https://assets.leetcode.com/uploads/2021/08/26/image-20210826114243-1.png)

**Input**: original = [1, 2, 3, 4], m = 2, n = 2  
**Output**: [[1, 2], [3, 4]]  
**Explanation**: The constructed 2D array should contain 2 rows and 2 columns.  
The first group of n=2 elements in the original array, [1, 2], becomes the first row in the constructed 2D array.  
The second group of n=2 elements in the original array, [3, 4], becomes the second row in the constructed 2D array.

So, I think I need to check for validation at the start—whether it’s possible to make a 2D array or not. If not, return an empty 2D array.

I’ll use Python:

```python
def construct2DArray(original, m, n):
    if m * n != len(original):
        return []
    
    result = []
    for i in range(m):
        result.append(original[i * n:(i + 1) * n])
    
    return result
```

Let’s break it down. This part checks for the condition:

```python
if m * n != len(original):
    return []
```
And this part fills the array. For i = 1, this slices original[1 * n:2 * n], which is original[n:2 * n]. This forms the second row, and so on

```python
for i in range(m):
    result.append(original[i * n:(i + 1) * n])
```

Finally, we return the array. Hey, it seems like I’ve done this same question before somewhere, but I can’t remember.

### I Joined Some Awesome Communities

Today, I joined the HackerOne, OffSec, and PortSwigger Discord communities. I just poked Blaklis a bit in the H1 Discord, and he shared his DEFCON slides, which are open in my next tab. I have to check them out. My Discord username is xfi1337, so say hi if you’re reading this.

### End?

Yeah, that’s it. I’m thinking of making a YouTube video or something, but I’m so tired right now. There was no practical hacking today because I spent too much time doing MMA, and my back is hurting a bit. It’s common now—I live with pain. So, I’ll write some random Python scripts, stalk GitHub repos, beg for jobs on LinkedIn, and then sleep. Can I call this day productive? I think I’m missing something. Give me the energy to go and hit HTB again, but I’ve lost the motivation. So here’s the thing: on Day 2, I’ll come back harder. And if anyone is reading this, please remind me to write that practical race condition article if I haven’t. Bye, take care, let’s goooo.

I forgot to mention that I’m also learning four new languages: Russian, Japanese, Spanish, and Chinese. I’m pretty good at Russian because of, well, some personal reasons, haha. But with the others, I’m really struggling. So, if anyone knows these languages, please connect with me!

*Yo bebo, tú bebes, él bebe.*
