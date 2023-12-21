---
title: "Buffer Overflow Program"
layout: post
---
Summary:
  1. Writing a Buffer Overflow Program
  2. Run Code to Demonstrate Buffer Overflow
  3. Analyzing and Modifying Overflow Code

To begin this exercise I launched a Kali Linux virtual machine and logged into the root account. Following log in, I opened Text Editor and began typing a script that follows:

![image](https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/62685a3a-fc94-4be3-b2cc-b4aa3239742e)

The file was saved as vuln1.c and compiled with the following command:
  - gcc vuln1.c -o vuln1

Once compiled, I was able to run the program entering:
  - ./vuln1
  - and entering 1-9 when prompted to "Enter the values".

This resulted in a buffer overrun because 9 elements were chosen as an input into a buffer of 8.

After analyzing and modifying the code the resulting code was as followed:

<img width="644" alt="Screenshot 2023-11-30 171321best" src="https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/361bec8d-f8da-4c87-836c-45ead9f75e11">

Block 1: This block sets up the variables called i, num, and an array/list of characters 'buffer' of up to 8 in length.

Block 2: This block prompts the user to enter a number of integers to put into the array.

Block 3: This block ensures there will not be a buffer overrun.

Block 4: This block asks the user for the integers to use and assigns them one by one into the array 'buffer'.

Block 5: This block prints the integers entered previously by the user

Block 6: Ends the program

The program is now fixed.




