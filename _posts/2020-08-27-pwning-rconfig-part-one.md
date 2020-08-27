---
layout: post
title: Pwning rConfig part I
---
**Pwning rConfig: part one**


Hi everyone. I&#39;ve been quite busy lately, but some weeks ago I decided to review the security of a software called rConfig version 3.9.5 ([www.rconfig.com](http://www.rconfig.com/)) which is a Network Monitoring tool and I found several vulnerabilities. So let&#39;s take a look at them ;)

**LFI 1**

Local file disclosure in /lib/crud/configcompare.crud.php, when comparing the parameter path\_a to path\_b, the file specified in path\_a is disclosed if both files are completely different. Here we can see the contents of /etc/passwd


![](https://i.imgur.com/GRiS3qF.png)
![](https://i.imgur.com/zPoqjGv.png)

**Arbitrary file deletion**

Arbitrary file deletion in /lib/ajaxHandlers/ajaxDeleteAllLoggingFiles.php. You can delete any file with an extension by specifying the file with the path parameter and the extension with the ext extension

![](https://i.imgur.com/ZddQdNh.png)

![](https://i.imgur.com/VjLjf77.png)

**Server-Side Request Forgery**

Server-Side Request Forgery in /lib/ajaxHandlers/ajaxDeviceStatus.php, you can open a connection to the inside of the machine with the deviceIpAddr parameter and the connPort parameter.

![](https://i.imgur.com/zi1zIbo.png)

**OPEN PORT:**

![](https://i.imgur.com/hY2DgHv.png) 

**Error:**

![](https://i.imgur.com/stK493D.png)

![](https://i.imgur.com/u3rVZ7m.png)

![](https://i.imgur.com/jS2O4e1.png)

**XSS**

Cross-Site Scripting in /devices.php > Add device, introduce a payload such as <svg onload=alert(1)> in the Model field and clicking Save (it&#39;s needed to fill the rest of fields with info). Then visiting /devicemgmt.php?deviceId=1&amp;device=devicename

![](https://i.imgur.com/6X7HWph.png)

**XSS 2**

Cross-Site Scripting in /commands.php > Add command, introduce a payload such as <svg onload=alert(1)> in the Command field and click Save.

![](https://i.imgur.com/aBwu34Q.png)

**XSS 3**

Cross-Site Scripting in /snippets.php > Add snippet, introduce a payload such as <svg onload=alert(1)> in the Snippet field and click Save(fill the rest of fields first).

![](https://i.imgur.com/5aYwSAy.png)

**Privilege escalation 1**

Using sudo zip:

![](https://i.imgur.com/PuLwT3i.png)

**Privilege escalation 2**

By doing sudo crontab -e and then :!/bin/bash

**Arbitrary file read:**

Following this we can read any privileged file: [https://gtfobins.github.io/gtfobins/tail/](https://gtfobins.github.io/gtfobins/tail/)

So those are some of the vulns I found during the research, hope you enjoyed the article. Back with the second part soon :)
