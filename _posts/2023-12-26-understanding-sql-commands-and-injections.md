---
title: "Understanding SQL Commands & Injections"
layout: post
---
Summary:
  1. Basic SQL Commands
  2. Querying with SQL
  3. Deleting with SQL
  4. SQL Injection
  5. Using SQLmap

To begin this exercise I launched a Kali Linux virtual machine and logged into the root account. Following log in I opened a new terminal window and started the mysql service by entering the command:

  - service mysql start

and logged into the mysql database with the command:

  - mysql -u root

Once logged into the mysql database, I created a new database test by entering:

  - create database test;

and used the new database by entering the command:

  - use test;

Now that the new database is used, I created a new table within the test database for users and populate it with the command:

  - create table users (name varchar (30), account integer, balance decimal (10,2));

Once the table is created, I began to add some data into the users table by entering the command:

  - insert into users values ('John', 123, 10.00);
  - insert into users values ('Joe', 456, 20.00);

Once some users are entered into the table, I created another table labeled "personal" by entering the command:

  - create table personal (name varchar(30), address varchar(30), city varchar(20), telephone bigint);

and entered some data into the personal table by entering:

  - insert into personal values('John', '1313 Mockingbird Lane', 'Mockingbird Heights', 3105552368);
  - insert into personal values('Joe', '1313 Cemetery Lane', 'Greenbrier', 1313131313);

To view the data from the personal table I entered the command:

  - select * from personal;

![image](https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/caeb99a7-ff72-416b-8ee0-ae317c9921e8)

Once the tables are created I began to understand querying with SQL by testing commands such as:

  - select name, balance from users; / using the test database I pulled the names and balance of users
  - select name, telephone from personal; / using the personal table I pulled names and telephone numbers
  - select users.name, users.balance, personal.telephone from users join personal where users.name=personal.name; / retrieves data across both test and personal tables

And learned to delete entire databases and tables by using the commands:

  - delete from personal where name='Joe';
  - drop table personal;
  - drop database test;

Finally, I began to understand SQL injection. To begin I opened a web browser and typed the exercise given IP address into the address field and pressed enter.

Once the web page loaded, I launched the training application DVWA (Damn Vulnerable Web Application).

Once on the DVWA application, I logged in using the provided username and password.

To test if the application is vulnerable to SQL injection I simply entered a true statement into the user ID text field such as 1=1. 

At this point I noticed that a query was sent to the database that executed select first name, last name from a table where the user id is equal to 1.

Following this, I displayed all records that are false by entering 1' or '0'=' 0, and then attempted to pull database information and the user of the database by entering 1' or 1=1 union select database(), user()#.
This returns the database name of DVWA and its user dvwa@localhost. 

Then I attempted to pull the database version by entering, 1' or 1=1 union select null,version()# and identified the tables in the database by entering, 1' or 1=1 union select null, table_name from information_schema.tables#.

Lastly, I attempted to see if any password fields are associated with the users table, by entering the command:

  - 1' or 1=1 union select user, password from users#

the results follow.

![image](https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/b8603f68-f35e-48a6-8914-7aea992f21d2)



