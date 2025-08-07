https://portswigger.net/web-security/sql-injection/lab-login-bypass

Lab objective:  `Logs in to the application as the administrator user.`

# Lab: SQL injection vulnerability allowing login bypass

After opening the lab we see the home page.

![[Sqli Lab 2.png]]

Now we will go to my account section.

![[Sqli Lab 2-1.png]]

This lab contains a SQL injection vulnerability in the login function.
So, here we need to input `administrator` information. But we don't know the information.

Generally SQL query is: `FROM * SELECT <TABLE NAME> WHERE USERNAME = '<USERNAME>' AND PASSWORD = '<PASSWORD>'`

Now if we input `administrator'--` The SQL query look like this: `FROM * SELECT <TABLE NAME> WHERE USERNAME = 'administrator'--' AND PASSWORD = '<PASSWORD>'`

So After `--` rest of the query will comment-out as a result the query will: `FROM * SELECT <TABLE NAME> WHERE USERNAME = 'administrator'--`

So we will login as the administrator user.

![[Sqli Lab 2-2.png]]

