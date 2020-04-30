---
layout: post
title: Certified Red Team Professional Review
---
**My experience with PentesterAcademy's Active Directory Attack and Defense course**

Hi everyone, it has passed some time since I last wrote an article. To be honest I thought about doing one about my experience with OSCP some months ago, but I forgot totally to do it :P Since then many things happened: got my OSWP, also CREST CRT and finally, CRTP which was really cool.

![alt text](https://www.pentesteracademy.com/img/adm.jpg "Logo Title Text 1")

First of all, what is the Certified Red Team Professional course? This the description in https://pentesteracademy.com

```Attacking and Defending Active Directory Lab is designed to provide a platform for security professionals to understand, analyze and practice threats and attacks in a modern Active Directory environment. The lab is beginner friendly and comes with a complete video course and lab manual. The course and the lab are based on our years of experience of making and breaking Windows and AD environments and teaching security professionals.```

```The lab is tightly integrated with the course and is designed as a practice lab rather than a challenge lab. We cover topics like AD enumeration, trusts mapping, domain privilege escalation, domain persistence, Kerberos based attacks (Golden ticket, Silver ticket and more), ACL issues, SQL server trusts, Defenses and bypasses of defenses.```

**The labs**

When I started in the labs, I realized the great difference with OSCP. In OSCP you are given some videos and a PDF and you can do whatever you want in the labs. That's good if you already have some experience. In the case of CRTP the labs go along with the video course. You learn every concept from the videos and after, you can practice by yourself with some exercises called Learning Objectives. This makes CRTP very useful for people with almost no experience in Active Directory (which was actually my case). The concepts are explained very well in the videos and if you get stuck in any of the Learning Objectives, you can always check the solution videos or the PDF. This labs are mainly thought (in my opinion) to get into a real attacker mindset, I mean, after every step you need to go back to enumeration and try to use things you had/discovered before along with whatever you have just compromised (ex: an user, or a box). I learnt many new things, and also made me re-think about some I already knew in a different perspective. For example, before CRTP I only thought SQL Servers could be compromised as Internet-facing assets with some password reuse, but thanks to the course I know know how, for example, I could use a SQL server to get code execution in a different domain.
Also, it is worth noting that PentesterAcademy has a great email support, and if you have any issue or even doubts about the course materials, you just need to email them and you will get a quick reply.

**The exam**

![alt text](https://media3.giphy.com/media/12vJgj7zMN3jPy/giphy.gif?cid=ecf05e4709f5186ecb92a0880b0ac53bc383da9396359cf0&rid=giphy.gif "whatever")

The exam is a 24-hour challenge in which you have execute code in 5 machines to pass. After that you have 48 hours to write the report. You are given access to a machine in a VPN 

For me it was stressful because I think I did my enumeration too exhaustive and I spent like 5 hours with the initial enumeration. I actually overthinked a lot. Pro Tip: Don't do that.

In my case I wanted to have everything ready so I set up a CherryTree file with every, really, every, step I needed to take. After those 5 hours I had plenty of screenshots of all my enumeration, so even if I missed anything initially, I could go back to it. This was actually very handy when it came to writing the report ;) 

After those 5 hours, I was SYSTEM in my computer and had my first box compromised (this was after many trial and error). I started the exam at 12 o'clock here in Spain, so that was around 5 PM. I got really stuck with the second box, trying really complicated stuff. It ended up to be that I overlooked something in my enumeration (this box almost ran me out of time). Facepalm for myself :P 

Finally got my third box, and I think I knew how to do the rest, but I preferred to use the little time of VPN access I still had to write the report, and to ensure a dozen times that everything was alright, every screenshot, every command I used.

So I sent the report and was like this for like a day: 

![alt text](https://media3.giphy.com/media/Jhzvy6CFpKQvK/giphy.gif?cid=ecf05e47a3623a1a5c5e70415ebe8acfa6ecb64d92c700d2&rid=giphy.gif "w")

After a day of thinking what I could I've done better and praying to pass, I finally got this: :)

![alt text](https://i.imgur.com/zJ52ojL.png)

I was so tired to celebrate enough that day, but the following..that was a party :P

My takeaways from both the course and the exam:

1) Don't rush through the course, if you have enough time, do the Learning Objectives multiple times.

2) Ensure you know all the concepts, the situations you are presented in the course are just examples, the techniques can be used in multiple ways, and even combining some together.

3) Enumerate, enumerate, enumerate. CherryTree is your friend.

After all the effort I can now say I am a Certified Red Team Professional :)

![alt text](https://www.pentesteracademy.com/img/redteamprofessional.png)


Here you have some useful links that have helped me in the journey: 

-https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology and Resources/Active Directory Attack.md

-https://www.labofapenetrationtester.com/2016/02/getting-domain-admin-with-kerberos-unconstrained-delegation.html

-https://adsecurity.org/

-https://github.com/HarmJ0y/CheatSheets/blob/master/PowerView.pdf

That was all for now, let me know if you found it useful :) Bye bye ;)


