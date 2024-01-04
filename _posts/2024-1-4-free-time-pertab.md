---
title: "Python Free Time Project - Periodic Table of Elements"
layout: post
---
Summary: 

This program allows the user to search elements from the periodic table by the name, atomic number, or symbol.

```py
import pandas as pd

print("===============================================")
print("||         Please select an option:          ||")
print("===============================================")
print("|| 1. Search an Element by Name.             ||")
print("|| 2. Search an Element by Atomic Number.    ||")
print("|| 3. Search an Element by Symbol.           ||")
print("===============================================")
search = int(input("Your choice: "))

def main():
    data = pd.read_csv('Desktop\\Periodic Table of Elements.csv')
    
    if search == 1:
        choice = input("Please enter the name of the Element: ")
        data = data.set_index('Element')
        print(data.loc[choice])

        print(" ")
        print(" ")
        print("===============================================")
        print("||     Would you like to search again?       ||")
        print("===============================================")
        print("||  1. Yes                                   ||")
        print("||  2. No                                    ||")
        print("===============================================")
        again = int(input("Your choice: "))
    
        if again == 1:
            main()
        elif again == 2:
            exit()
        else:
            print("Invalid option. Exiting...")
            exit()

    elif search == 2:
        data = data.set_index('AtomicNumber')
        choice = int(input("Please enter the Atomic Number of the Element: "))
        print(data.loc[choice])

        print(" ")
        print(" ")
        print("===============================================")
        print("||     Would you like to search again?       ||")
        print("===============================================")
        print("||  1. Yes                                   ||")
        print("||  2. No                                    ||")
        print("===============================================")
        again = int(input("Your choice: "))
    
        if again == 1:
            main()
        elif again == 2:
            exit()
        else:
            print("Invalid option. Exiting...")
            exit()
        
    elif search == 3:
        data = data.set_index('Symbol')
        choice = input("Please enter the Symbol of the Element: ")
        print(data.loc[choice])

        print(" ")
        print(" ")
        print("===============================================")
        print("||     Would you like to search again?       ||")
        print("===============================================")
        print("||  1. Yes                                   ||")
        print("||  2. No                                    ||")
        print("===============================================")
        again = int(input("Your choice: "))
    
        if again == 1:
            main()
        elif again == 2:
            exit()
        else:
            print("Invalid option. Exiting...")
            exit()

main()
```

Output Examples:

<img width="307" alt="Name" src="https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/47cdf41d-608c-4084-b1c1-342a8d92c98e">

<img width="321" alt="Atomic Number" src="https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/98788e41-8601-4449-9e9b-744d40e882a4">

<img width="307" alt="Symbol" src="https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/f1d29ed0-b16f-49c1-820c-70d787d879e4">





