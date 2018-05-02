---
layout: post
title:  "VulnHub: Necromancer! by @Xerubus"
date:   2018-04-10 16:46:00
categories: CTF VulnHub WriteUp
---

In this post, I will walk you through my methodology for solving a Vulnhub VM known as Necromancer that was my first machine on a CTF challenge and I have learned a lot with it.


The machine is intended to teach beginners about the basics of CTF challenges.
There are 11 flags to collect on your way to solving the challenge.

The end goal is simple… destroy The Necromancer!
![necromancer ascii]({{ "/assets/images/necromancer-00.png"}})
VM is designed to DHCP auto assign so we typically track the VM's IP running netdiscover.
![necromancer ascii]({{ "/assets/images/necromancer-01.png"}})
First off, i perform a TCP SYN scan via nmap to identify open ports on the target machine. I usually perform a scan for ALL ports during CTF challenges to check for services that are not utilizing the TOP 1000 ports.
![necromancer ascii]({{ "/assets/images/necromancer-02.png"}})
The scan gives us nothing. It seems that all TCP ports are closed or filtered. So, I try a UDP scan using nmap again.
![necromancer ascii]({{ "/assets/images/necromancer-03.png"}})
Port 666 is open! Let' try a Netcat to see what is running in that port.
![necromancer ascii]({{ "/assets/images/necromancer-04.png"}})
No matter how many times we hit enter, we get the same reply- “You gasp for air! Time is running out!”. Is there something happening that we can’t see?
I decide use the wireshark to sniff the traffic to see what’s happening under the hood.("tcpdump host \<ip\>" is another option here)
![necromancer ascii]({{ "/assets/images/necromancer-05.png"}})
Looking at the log, we can see a connection being made from the Necromancer’s IP address to our IP address. The connection is destined to port 4444.
This can be another port on our target. Lets use netcat once again to see the data being transferred.
![necromancer ascii]({{ "/assets/images/necromancer-06.png"}})
We get a text dump in return. It has capital characters, small characters and numbers as well. This has to be a base64 encoded text.
So i decode it using the base64 -d command in terminal to make the things more readable.
![necromancer ascii]({{ "/assets/images/necromancer-07.png"}})
![necromancer ascii]({{ "/assets/images/necromancer-08.png"}})
<b>First Flag captured!</b> The flag1 text seems to be a md5 hash so we decrypt it at www.hashkiller.co.uk. It decrypts to “opensesame”.
Based from the hint given on the message, we need to “chant” the string of flag1 to UDP 666 via netcat.
![webimage and text]({{ "/assets/images/necromancer-11.png"}})
<b>Second Flag Captured!</b>
Another hint. Numeral 80 reminds us of port 80 used for http. Let’s fire up the victim machine’s IP to our browser on port 80.
![webimage and text]({{ "/assets/images/necromancer-09.png"}})
Reading the message doesn’t make any sense so there must be something hidden in the picture.
Let’s download it and try to analyse it using binwalk(I could have used Foremost here too).
![binwalk result]({{ "/assets/images/necromancer-10.png"}})
So we discover that the image is actually a zip archive and use binwalk to extract all the files.
Upon unzipping the file we get a txt file named feathers.txt which again contains a base64 text. We it and get our 3rd flag along with a clue /amagicbridgeappearsatthechasm. Seems like a directory decode.
![base64 unziped]({{ "/assets/images/necromancer-12.png"}})
<b> Third Flag Captured! </b> Let’s browse to the /amagicbridgeappearsatthechasm directory.
![new directory acess]({{ "/assets/images/necromancer-13.png"}})
Opening the directory in our browser and running basic steganalysis tools like strings, unzip, exif, steghide, etc will lead us nowhere.
It only tells us that we need a magical item that could protect us from the necromancer’s spell.


So I decide google for “magic items wiki” to find some good stuff and make a custom dictionary with all the words on this wiki page. I will use cewl for this.
![new directory acess]({{ "/assets/images/necromancer-14.png"}})
Found a directory  /amagicbridgeappearsatthechasm/talisman!
Next, let’s browse to /talisman directory.  Upon browsing to this site, we will be prompted with a file download dialog box. Let’s download the file.
![new directory acess]({{ "/assets/images/necromancer-15.png"}})
![new directory acess]({{ "/assets/images/necromancer-16.png"}})
Chmod +x to make executable…
when run it gives an interesting result.
![new directory acess]({{ "/assets/images/necromancer-17.png"}})























