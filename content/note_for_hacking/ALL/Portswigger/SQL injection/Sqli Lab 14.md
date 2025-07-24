https://portswigger.net/web-security/sql-injection/blind/lab-time-delays

Lab objective: `exploit the SQL injection vulnerability to cause a 10 second delay.`

This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.

The results of the SQL query are not returned, and the application does not respond any differently based on whether the query returns any rows or causes an error. However, since the query is executed synchronously, it is possible to trigger conditional time delays to infer information.

# Lab: Blind SQL injection with time delays

1. `TrackingId=WZ4yqDPUYMn5Jgve'|| ( SELECT pg_sleep(10)) ||'` we use this because database was `PostgreSQL`. and our lab is solve.
