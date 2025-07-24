https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-subtly-different-responses

To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page.

username and password list given in the lab.

# Lab: Username enumeration via subtly different responses

1. First we try to login with invalid username and password. Then we get the massage `Invalid username or password.`
2. Send the request to intruder tab and brute-force on username section. And then negative filter using this `Invalid username or password.` and we get only one username is `auto` (Change every-time)
3. Now we will use this username and brute-force the password. We get `Status code 302` on this password `zxcvbnm` (Change every-time)
4. Now login using the username and password to solve the lab.