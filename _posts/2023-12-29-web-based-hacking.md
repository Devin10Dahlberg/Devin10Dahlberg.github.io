---
title: "Web-Based Hacking"
layout: post
---
Summary:
  1. Footprinting and Enumerating
  2. Perform an OWASP Top 10 Attack
  3. Cookie Manipulation

To begin this exercise I launched and logged into an administrator account on a Windows OS virtual machine.

Following log in, I launched an application called "Vega", and familiarized myself with different panes, and options.

To begin the exercise, I clicked "Start New Scan" and when prompted entered the IP address that was provided to me for this exercise. 

This scan revealed to me the different vulnerabilites found categorized in High, Medium, and Low levels of vulernability.

I then focused my attention to the High category and located the results labeled, "Session Cookie Without HttpOnly Flag", and under this drop drop I located /webcal/login.php.

Here I was able to find information with specific details of the vulnerability, how to fix the problem, and source information about the vulnerability:

![image](https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/f8ed3d93-2e38-4d5e-94be-acec9c946001)




For the next portion of the exercise, I practiced web hacking using the Web Goat platform and attempted to access the account "alice".

To begin, I launched a window of Firefox and in the address bar I entered a given IP address, and click OWASP WebGoat.

From this point, I logged into the WebGoat server and clicked "Start Webgoat".

I then found the tab labeled, "Session Management Flaws" and clicked "Spoof an Authentication Cookie" and logged into this portion of the website with the username "webgoat".

Once my identity was remembered, I opened Web Developer, and navigated to Storage Inspector.

Here I located, and opened AuthCookie to view the contents of the cookie in the Data Pane.

<img width="388" alt="image" src="https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/b26a0525-4e8c-45ef-a2bd-a40e3f16d73c">

I then copied the Value field associated with the AuthCookie and opened a Notepad++ file.

At this point, I typed the username to the account I previously logged into and pasted the value data next to the username and saved the file.

<img width="739" alt="image" src="https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/863cfdd7-17b0-4514-a049-6d17bf24930c">

Next, I logged out of the account "webgoat" and logged into the account "aspect" and repeated the previous steps until the username and value data were in the same file as before.

<img width="494" alt="image" src="https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/db5f29a2-a6f6-425a-ad54-f356f38fcff2">

From this point, I recognized that the first five characters of the value data were identical which means I only need to decode the data after 65432.

I then noticed the data is encoded by reversing the username and then shifting one letter alphabetically.

From here, I added another line to Notepad++ file and the username is "alice" followed by the data value 65432fdjmb. This is because fdjmb is equivalent to alice reserved and shifted one letter similar to the data in the previous accounts.

<img width="569" alt="image" src="https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/453919eb-cb97-4015-a497-b7326558db3d">

Next, I returned to Firefox; however, this time in Storage Inspector in the AuthCookie field I replaced the value data provided to the account "aspect" with the value data I created for "alice".

This triggered a window to appear which allowed me to refresh the page and be logged into the account "alice".

![image](https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/8bfa8b95-189b-4a06-ac81-686b030e1884)








