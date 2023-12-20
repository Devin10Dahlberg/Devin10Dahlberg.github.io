---
title: "Packet Crafting with Scapy"
layout: post
---
Summary:
  1. Creating Packets with Scapy
  2. Sending Crafted Packets

To begin this exercise I logged into the root account of a Kali Linux virtual machine. Following login I initialized the Scapy application through terminal. 
Following the launch of Scapy, I began to build a simple IP packet using the RFC 791 to define the IP protocol by entering the following commands:

 - ip=IP(ttl=10) / sets the time to live for the IP packet
 - ip.dst="(IP address)" / changes the IP destination
 - ip.src="(IP address)" / changes the IP source address
 - del(ip.ttl) / removes the TTL and sets it to the default TTL specified in the RFC
 - ip/TCP() / adds additional protocol layers by adding TCP on top of IP
 - tcp=TCP(sport=1025, dport=80) / adds some information to the TCP protocol fields
 - Ether()/ip / adds an ethernet layer

![image](https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/7a97d929-cc19-4392-bbfa-5bbd385f7dfe)

Once the packet is built, I launched a new terminal and opened the application Wireshark. Within the Wireshark window I selected the ethernet interface required and began to start capturing packets.
Navigating back to the terminal window with the Scapy prompt, I generated a single ICMP packet to be sent to the OWASP virtual machine by entering the command:

  - packet=sr1(IP(dst="(IP address)")/ICMP()/"XXXXXXXXXXX")

Then nagivated back to the Wireshark window to see that the Scapy packet was successfully sent through an ICMP request to the OWASP virtual machine.

Switching back to the terminal window with the Scapy prompt. I ran the command:

  - packet=sr1(IP(dst=”(IP Address)”)/TCP(dport=80,flags=”S”))

to initiate a SYN scan on a single port.

Switching back to the Wireshark window, I analyzed the output and was able to recognize that a SYN packet was sent with SYN and an ACK packet was recieved indicating that port 80 is open.

![image](https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/5da5bf75-936c-402c-bc52-43cc51a497ae)





