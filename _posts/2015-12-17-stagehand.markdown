---
layout: post
title: "Introducing: Stagehand"
date: 2015-12-17 12:00
authors: [logan]
description: For a course in Software Systems at Olin College of Engineering, we created Stagehand, a stager written in C and Assembly. Stagehand is the first open-source stager to use a third-party site (i.e. Pastebin) as a repository for a payload of malware.
tags: [security, cybersecurity, stager, stagehand]
---

{% assign author = site.authors[page.author] %}

In case you couldn't tell from [last month's post](http://ungineers.com/2015/11/28/metasploit-exploit-payload-sizes.html) about Metasploit payload sizes, my friend and fellow Ungineer Dakota is a huge software security nerd. (I shouldn't poke fun - everyone needs a hobby, and his is significantly cooler than (ahem) writing about baseball statistics.) So when the two of us wound up on a Software Systems team with our mutual friend Austin, and we needed an idea for a final project, he turned to Austin and I and pitched an idea. Why not try writing a stager?

Those loyal readers who actually clicked the link to last month's post in the paragraph above - you da real MVPs - should now know a little bit about stagers. The short version, for the rest of the unwashed heathens: a "stager" is a tiny, robust piece of software that is delivered as a payload to a target computer by an "exploit" (a malicious piece of software that takes advantage of vulnerabilities in the target's cyber-defenses to gain some control over it). Stagers must be tiny for the same reason that they exist: most exploits can only deliver very limited quantities of malicious code. Stagers are deployed to overcome this challenge. Cyber-attackers use stagers to establish a toehold on a target machine, then pull much nastier and more fully-featured malware across the network and execute that.

Stagers are pretty useful tools in the proverbial hacker's toolbelt, but they're not without weaknesses. For instance, at the step in their exeuction where they reach out to a server and pull down some executable code, they're pretty visible. A good security system can spot the outbound network traffic going to an unfamiliar server and will immediately suspect that something is up. Of course, once stager-using cyber-attackers realized that their natual enemies the sysadmins were onto their games, they kicked things up a notch. Earlier this year, hackers [were observed](https://securelist.com/blog/research/69490/dont-feel-left-out-ransomware-for-it-security-enthusiasts/) using Pastebin to temporarily host encrypted malware for their stagers to access. A request to a well-known website that allows for unlisted storage of arbitrary text, like Pastebin, looks a lot less suspicious than a request to some random server. 

Those of you familiar with the world of cyber-security are also probably familiar with the use of the terms "white hat" and "black hat" to describe (respectively) hackers with good intentions who report vulnerabilities and bugs so that they can be fixed... and hackers with bad intentions who exploit vulnerabilities to run malicious code. Dakota may be an evil-lookin' dude, but he's very much a white hat hacker - he works as a penetration tester at Black Hills Information Security, so it's literally his job. When he saw that there was a stager technique in the wild which had yet to be reproduced by an open-source programmer, i.e. pulling down data from Pastebin, and when he was presented with a class project for which programming a stager was a reasonable choice, he came to a natural white-hat conclusion: we should create such a stager and make it free for use by cyber-security researchers and friendly sysadmins everywhere. Thus Stagehand was born.

The first chunk of Stagehand isn't actually part of a stager, but a support script that makes stager use possible. This small Python script Base64-encodes some arbitrary shell code, uses Pastebin's API to upload it to an unlisted temporary page, grabs the URL of that page, and templates it into Stagehand proper. Once Stagehand has the URL of the payload it'll ultimately retrieve, its stager must be deployed to a target machine, whether by security exploit (as a cyber-attacker would) or by downloading it from Git (as a researcher might). Running the executable file generated by the Python script and the Stagehand makefile will cause the deployed stager to pull down the code from Pastebin, decode it, and execute. 

From a technical perspective, the biggest challenge of writing Stagehand was getting the stager to be as small as possible. A good chunk of said stager is written in assembly, which was a new and interesting challenge for our team. We also use some EXE compression tricks to shrink the final executable. When all's said and done, our stager clocks in at around 6 KB - still too big for most exploits, but small enough to get the point across, we think. Here's a pretty picture of Stagehand executing arbitrary code it pulled down from Pastebin in a Windows VM:

{:.center}
![Stagehand Running In A Windows VM]({{site.url}}/assets/stagehand.png){: .image }

We hope that Stagehand is a useful tool for cyber-defenders everywhere to defend their cybers (or at least to better understand the methods of those who would attack their cybers). Interested parties can inspect our code on [Github](https://github.com/DakotaNelson/stagehand/).
