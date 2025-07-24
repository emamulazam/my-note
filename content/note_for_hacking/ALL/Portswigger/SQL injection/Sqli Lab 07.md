https://portswigger.net/web-security/sql-injection/union-attacks/lab-determine-number-of-columns

Lab objective: `Determine the number of columns returned by the query by performing a SQL injection UNION attack that returns an additional row containing null values.`

# Lab: SQL injection UNION attack, determining the number of columns returned by the query

We know that this lab contains a SQL injection vulnerability in the product category filter.

Click product category filter then

1. Find the column number `category=Gifts' ORDER BY 3--`
2. To solve you should give the query is `category=Gifts' UNION SELECT NULL,NULL,NULL--`