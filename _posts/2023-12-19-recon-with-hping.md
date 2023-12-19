---
title: "Reconnaissance with Hping"
layout: post
---
Summary:
  1. Using Hping as an ICMP Utility
  2. Using Hping for Port Scanning

To begin this lab, I launched the Kali Linux virtual machine and logged into the root account. Following login, I opened terminal to begin crafting a packet.
With hping, a packet was crafted using ICMP as the protocol with the command:
  - hping3 -1 (IP address)
This returns several ICMP messages (ICMP Type 0 Default) that received a reply.

Once about six packets are transmitted, I stopped hping from running and tested out a different ICMP type using a timestamp ICMP Type 13 by entering the command:
  - hping3 -c 3 -1 -V -C 13 (IP address)
This returns a reply with a timestamp that confirms the target is there.

You could also preform traceroute functions using ICMP by entering the command:
  - hping3 -c 5 -T -1 -V (IP address)
![image](https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/73ee3501-2115-4439-8e0a-7ae1c57d8f73)

Now that I am familiar with ICMP utilities using hping, I begin to explore using hping for port scanning.
To begin, I opened a second terminal window and began to start capturing packets using the command:
  - tcpdump -i eth0
and let the capture run in the background while proceeding.

Hping can craft packets that send various TCP flags set to test ports being scanned. To demonstrate this I sent a packet with SYN from a source port of 5151 by using the command:
  - hping3 -S -c 1 -s 5151 -p 80 -V (IP address)
After this command is entered, I am able to switch back to terminal that is running tcpdump and notice that a SYN flag was sent with a received Reset flag.

Once this was noted, I switched back to the command terminal and begin to try the SSH Port 22 against the firewall by running the command:
  - hping3 -S -c 1 -s 5151 -p 22 -V (IP address)
This resulted in a one-hundred percent packet loss due to port 22 being closed on the firewall.

Since this was the result, I decided to run a port scan against the firewall using a defined range with the command:
  - hping3 -S -8 20-80 -c 1 -s 5151 -V (IP address)
The results informed me that both port 53 and 80 are open.
![image](https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/f152445a-e6a3-4271-b8cc-425ea2b26849)



