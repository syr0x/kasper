---
layout: post
title:  "VulnHub: Necromancer! by @Xerubus"
date:   2018-04-10 16:46:00
categories: CTF VulnHub WriteUp
---

In this post, I will walk you through my methodology for solving a Vulnhub VM known as Necromancer that's was my first machine on a CTF challenge i have learned a lot with her.
The machine is intended to teach beginners about the basics of CTF challenges.
There are 11 flags to collect on your way to solving the challenge

The end goal is simple… destroy The Necromancer!
![necromancer ascii]({{ "/assets/images/necromancer-00.png"}})
VM is designed to DHCP auto assign so we typically track the VM's IP with netdiscover use.
<img1 netdiscover>

First off, i perform a TCP SYN scan via nmap to identify open ports on the target machine. I usually perform a scan for ALL ports during CTF challenges to check for services that are not utilizing the TOP 1000 ports.
<img2 nmap tcp>

The scan gives us nothing. So, i try a UDP scan using nmap again.
<img3 nmap udp>






