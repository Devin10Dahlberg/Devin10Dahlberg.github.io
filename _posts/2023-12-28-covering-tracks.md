---
title: "Covering Your Tracks"
layout: post
---
Summary:
  1. Using NTFS Streams
  2. Finding hidden files ADS Spy
  3. Extracting hidden files using OpenStego
  4. Extending Linux File Attributes to hide data
  5. Covering tracks by deleting Linux logs

I began this exercise by launching a Windows OS virtual machine and logging into the Administrator account. 

Once inside, I navigated to the Local Disk (C:) properties and created a folder on the desktop named Lab23.

In the C Drive I then nagivated to the Windows folder, then the System32 folder, then to the am-et folder which held a file named calc.exe which is the Calculator executable. 

I copied the file and pasted it inside the newly created Lab23 file. 

Next, I opened command prompt and changed the focus directory to the Lab 23 file, and created a text file by typing: notepad lab23.txt

In the newly created text file I typed "This is a secret message hidden from the average user!", saved and closed.

Changing focus to command prompt I then typed:

  - type calc.exe > lab23.txt:calc.exe

This command hides calc.exe inside the lab23.txt file, thus I am able to delete the calc.exe file from the Lab 23 folder.

I then created a symbolic link between directories with the command:

  - mklink exploit.exe lab23.txt:calc.exe

![image](https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/4272a615-fe02-47a8-9bc6-b81313db944d)

Now, by entering the command: exploit.exe, the calculator application will be executed.

This simulates a malicious exploit that could be hidden in a file.



For the next portion of the exercise, I located hidden files using ADS spy.

First, I launched the application ADSSpy.exe and the ADS Spy main window appeared.

I then changed the configurations to my liking by prompting a Full Scan, Ignore safe system info data streams, and scan the system for alternate data streams.

This scan found hidden streams and I was able to removed them.

![image](https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/2462a60d-0941-4d2f-b74b-d348054cf7c8)



Next portion of the exercise, I extracted ADS files using OpenStego.

To begin I launched the OpenStego application, and chose a png file that I wished to open, and chose where I wanted the output message file to be sent to.

After the, the message file was successfully extracted from the cover file, I navigated to the file to view the results. 

The results were a repeating message that stated: "RANSOMEWARE!" continously.

Using ADS Spy, I was able to remove the malicious streams leaving just the message.

![image](https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/f294af57-1e3b-4778-b6b8-e398d49ef544)



For the next portion of the exercise, I practiced using extended file attributes on Linux to hide data.

To begin, I created a new text file named lab23.txt, and added the text I intended to hide in the extended attributes of the file with the command:

  - setfattr -n user.attribute1 -v “data hidden here” lab23.txt

and then added another attribute by typing:

  - setfattr -n user.attribute2 -v “data also hidden here” lab23.txt

Since the attributes are now set, they will not be seen by the user in the File Manager or in a file list.

To view the attributes, you can enter the command:

  - getfattr -d lab23.txt

![image](https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/f858362c-48b8-4432-86b0-4eedea1bac39)

For the final portion of the exercise, I practiced covering tracks by deleting Linux logs.

To begin, I opened a new terminal window and entered the commands:

  - last -f /var/log/btmp
  - last -f /var/log/wtmp

This command allows me to review the btmp and wtmp logs.

To remove this data and further cover our tracks, I entered the commands:

  - cat /dev/null > /var/log/wtmp
  - cat /dev/null > /var/log/btmp

to replace the directories with a blank file.

The next log I looked at is the sudo log by entering the commands:

  - sudo ifconfig
  - sudo grep sudo /var/log/auth.log

Then to remove the contents of this file, I entered the command:

  - cat /dev/null > /var/log/auth.log

The final but most important log I covered is the bash_history log.

To begin I entered:

  - cat .bash_history

to look at the list.

Then, to remove the data without deleting the file I entered:

 - root@kali:~# > .bash_history

Then checked to see if the data was cleared:

![image](https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/2541ae20-8f42-4131-83d5-4d8b0cb0af5d)

There are many other log files that can be used to prove attackers accessed the system; however, in this exercise, I focused on removing evidence of the attackers login and terminal activity.














