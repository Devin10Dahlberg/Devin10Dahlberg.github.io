---
title: "DNS Footprinting"
layout: post
---
Summary:
  1. Footprinting with nslookup
  2. Compare nslookup with dig

Part One:

I began this lab by logging into the root account of a Kali Linux virtual machine and familiarizing myself with the environment by running commands such as:
  - man nslookup / This allowed me to review the user manual page for nslookup.
  - nslookup -> server / This allowed me to determine my current lookup server.
  - server (IP address) / This allowed me to change the default server.
Once the default server was changed, I proceeded to see what the root domain in the lab environment resolved to by typing the domain lookup command.
This command returned the nameserver for the domain; however, by using the set type=a followed by the domain, I was able to return the IP address for the domain.

At this point, I switched to the OpenSUSE virtual machine and began familiarizing myself with nslookup commands on the OpenSUSE machine, while comparing nslookup to dig. To do this I entered the command:
  - dig @(IP address) (domain name) ns


