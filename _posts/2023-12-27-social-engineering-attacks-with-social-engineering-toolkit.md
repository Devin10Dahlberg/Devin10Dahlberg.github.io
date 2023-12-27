---
title: "Social Engineering Attacks with Social Engineering Toolkit"
layout: post
---
Summary:
  1. Using the Social Engineering Toolkit (SET)
  2. Modifying the SET Parameters
  3. Test the SET Attack

I began this exercise by logging into the root account of a Kali Linux virtual machine and opening a terminal window.

To begin, I opened the Social Engineering Toolkit (SET) by using the command:

  - setoolkit

and accepting the terms of service. On the SET main page, I was presented with a menu of choices and selected:

  - Social Engineering Attacks --> Website Attack Vectors --> Credential Harvester Attack Method --> Web Templates

and then entered the IP address of the Kali VM, and selected the Google template.

![image](https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/83113ff1-d2e2-4d21-8c19-52b86bd83964)

Next, I began modifying the SET Parameters. Starting with the redirect settings and URL, I entered the following command:

  - nano /etc/setoolkit/set.config

and edited the HARVESTER_REDIRECT and the HARVESTER_URL:

![image](https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/a9092f56-537e-43a7-a0ae-22429b4ef102)

Finally, I started to test the SET Attack by launching a OpenSUSE virtual machine and logging in. From this point I opened a Mozilla Firefox window and entered the VM IP address into the address field.

After a moment, a Google sign-in page appeared and in the Email field I entered: John Smith, and in the password field I entered: Letmein.

After this, I navigated back to the Kali VM and noticed in the terminal I had captured the Email and Password.

![image](https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/96da76f2-38f4-4211-a7bd-d5af3ef0b445)

I then ended and generated a report, and navigated to the /root/.set/reports directory and opened the report to view the contents of the file.

![image](https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/e129e683-37c6-494c-b1c8-ad48256ad9a5)




