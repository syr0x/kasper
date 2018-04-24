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
![necromancer ascii]({{ "/assets/images/necromancer-01.png"}})

First off, i perform a TCP SYN scan via nmap to identify open ports on the target machine. I usually perform a scan for ALL ports during CTF challenges to check for services that are not utilizing the TOP 1000 ports.
![necromancer ascii]({{ "/assets/images/necromancer-02.png"}})

The scan gives us nothing. It seems that all TCP ports are closed or filtered. So, i try a UDP scan using nmap again.
![necromancer ascii]({{ "/assets/images/necromancer-03.png"}})

Port 666 is open! Let' try a Netcat to see what is running in that port.
![necromancer ascii]({{ "/assets/images/necromancer-04.png"}})

No matter how many times we hit enter, we get the same reply- “You gasp for air! Time is running out!”. Is there something happening that we can’t see?
I decide use the wireshark to sniff the traffic to see what’s happening under the hood.("tcpdump host <ip>" is another option here)
![necromancer ascii]({{ "/assets/images/necromancer-05.png"}})

Looking at the log, we can see a connection being made from the Necromancer’s IP address to our IP address. The connection is destined to port 4444.
This can be another port on our target. Lets use netcat once again to see the data being transfered.
![necromancer ascii]({{ "/assets/images/necromancer-06.png"}})

We get a text dump in return. It has capital characters, small characters and numbers as well. This has to be a base64 encoded text.
So i decode it using the base64 -d command in terminal to make the things more easily to read.
![necromancer ascii]({{ "/assets/images/necromancer-07.png"}})

First Flag captured! The flag1 text seems to be a md5 hash so we decrypt it at www.hashkiller.co.uk. It decrypts to “opensesame”.
Based from the hint given on the message, we need to “chant” the string of flag1 to UDP 666 via netcat.
![necromancer ascii]({{ "/assets/images/necromancer-08.png"}})














