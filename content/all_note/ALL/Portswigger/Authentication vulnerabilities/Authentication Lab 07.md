https://portswigger.net/web-security/all-labs#authentication

This lab is vulnerable to username enumeration. It uses account locking, but this contains a logic flaw. To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page.

- [Candidate usernames](https://portswigger.net/web-security/authentication/auth-lab-usernames)
- [Candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords)

# Lab: Username enumeration via account lock

1. First we try to login with invalid username and password. Then we get the massage `Invalid username or password.`
2. After so many time sending this request nothing change. 
3. Now we will use intruder tab to brute-force the given username 5 time and remove the response with  `Invalid username or password.`
4. `ag` (change every-time) give use `You have made too many incorrect login attempts. Please try again in 1 minute(s).` so it is the valid username.
5. Now we will make password brute-force and remove the response `You have made too many incorrect login attempts. Please try again in 1 minute(s).` Then we will find our password and that is `1234`
6. Now login and complete the lab.