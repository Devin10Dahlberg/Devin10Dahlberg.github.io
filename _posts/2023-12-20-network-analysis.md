---
title: "Network Analysis"
layout: post
---
Summary:
  1. Capturing Traffic with tcpdump
  2. Analyzing Traffic with Wireshark

I began this exercise by logging to the root account of a Kali Linux virtual machine and running the command - man tcpdump - to get familiarized with the tcpdump command options in terminal. 
Once familiar with the commands I began the exercise by running the command:
  - tcpdump -i eth0 -s0 -w testdump.pcap / This command starts capturing packets and saving them as a .pcap format.

I left this command running and opened a new terminal to generate traffic with the OWASP virtual machine by entering the command:
  - smbclient -L (IP address) --option='client min protocol=NT1'

Followed by accessing the OWASPbwa server message block by entering the command:
  - smbclient \\\\(IP address)\\owaspbwa --option='client min protocol=NT1'

Once this is completed, I opened the web browser on Kali and typed the target IP address into the search bar to generate traffic this results were:

![image](https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/e11a328b-488f-4ec7-90d0-10ee6355bda1)

Next, I launched Wireshark through terminal and opened the testdump.pcap file through the Wireshark application and began to analyze the captured SMB shared traffic.
Using the "Follow TCP Stream" feature I was able to follow a conversation from the beginning to the end of a TCP connection such as follows:

![image](https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/0cb033be-ba3b-419e-9a4e-b7262e9720d6)

