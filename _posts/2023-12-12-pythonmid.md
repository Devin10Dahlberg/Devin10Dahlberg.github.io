---
title: "Python: Assignment Five"
layout: post
---

```py
#1. Write a while loop that asks the user to enter two numbers.
#2. Your variable names should be num1 for the first number and num2 for the second number.
#3. num1 and num2 should not be a negative number.  Use an if statement to force the user to enter a non-negative number for num1 and num2.
#4. The numbers should be added and the sum displayed.
#5. The loop should ask the user if he or she wishes to perform the operation again. If so, the loop should repeat, otherwise it should terminate.
#6. Output that you will provide to me: 1. Num1 2. Num2 3. Total (num1 + num2) Please format your output to look nice and provide text statements that are descriptive of the output being shown.

def main():
    addition()
    while True:
        choice = input("Would you like to do this again? Enter 'y' or 'n': ")
        if choice == 'y':
            addition()
        if choice == 'n':
            break

def addition():
    print("I am going to ask for two positive numbers and add them together.")
    print("I will print out the numbers and the total for you.")
    num1 = get_number("first")
    num2 = get_number("second")
    print(f"You entered",num1,"as your first entry.")
    print(f"You entered",num2,"as your second entry.")
    total = num1 + num2
    print(f"The sum of these two numbers is",total,".")

def get_number(entry_number):
    num = float(input(f'Please enter a non-negative number for your {entry_number} entry: '))
    while num < 0:
        print("Number cannot be negative. Enter a non-negative integer.")
        num = float(input(f'Please enter a non-negative number for your {entry_number} entry: '))
    return num
    
main()
    
```

<img width="1217" alt="Midterm Program" src="https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/10fe6f56-a528-4ac2-90d1-ec1d7b52eabc">
