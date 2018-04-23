---
layout: post
title:  "VulnHub: Necromancer! by @Xerubus"
date:   2018-04-10 16:46:00
categories: CTF VulnHub WriteUp
---

In this post, I will walk you through my methodology for solving a Vulnhub VM known as Necromancer that's was my first machine on a CTF challenge and i have learned a lot with her.


The machine is intended to teach beginners about the basics of CTF challenges.
There are 11 flags to collect on your way to solving the challenge.

The end goal is simple… destroy The Necromancer!
![necromancer ascii]({{ "/assets/images/necromancer-00.png"}})
VM is designed to DHCP auto assign so we typically track the VM's IP with netdiscover use.
<img1 netdiscover>

First off, i perform a TCP SYN scan via nmap to identify open ports on the target machine. I usually perform a scan for ALL ports during CTF challenges to check for services that are not utilizing the TOP 1000 ports.
<img2 nmap tcp>

The scan gives us nothing. It seems that all TCP ports are closed or filtered. So, i try a UDP scan using nmap again.
<img3 nmap udp>

Port 666 is open! Let' try a Netcat to see what is running in that port.
<img4 netcat connection trough port666>

No matter how many times we hit enter, we get the same reply- “You gasp for air! Time is running out!”. Is there something happening that we can’t see?
I decide use the wireshark to sniff the traffic to see what’s happening under the hood.("tcpdump host <ip>" is another option here)
<wireshark capture log>

Looking at the log, we can see a connection being made from the Necromancer’s IP address to our IP address. The connection is destined to port 4444.
This can be another port on our target. Lets use netcat once again to see the data being transfered.
<netcat listen>











