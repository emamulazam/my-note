https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-different-responses

To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page.

username and password list given in the lab.

# Lab: Username enumeration via different responses

1. First we try to login with invalid username and password. Then we get the massage `Invalid username` So we can easily enumerate username.
2. Send the request to intruder tab and brute-force on username section. Using `Grep-Match` of `Invalid username` we can find username is `auction` (Change every time) and response `Incorrect password`
3. Send the request to intruder tab and brute-force on password section. Using `Grep-Match` of `Incorrect password` we can find username is `qwertyuiop` (Change every time)
4. Using this username and password solve the lab.