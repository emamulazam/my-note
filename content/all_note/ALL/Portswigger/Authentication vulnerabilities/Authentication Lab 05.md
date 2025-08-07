https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-response-timing

To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page.

username and password list given in the lab. Your credentials: `wiener:peter`

To add to the challenge, the lab also implements a form of IP-based brute-force protection. However, this can be easily bypassed by manipulating HTTP request headers.

Identify that the `X-Forwarded-For` header is supported, which allows you to spoof your IP address and bypass the IP-based brute-force protection.

# Lab: Username enumeration via response timing

1. First we try to login with invalid username and password. And check response time.
2. Then check a valid username with a big password and check response time.
3. Every-time using `X-Forwarded-for` use different IP number.
4. Send the request to intruder tab and brute-force on username section. and mach the response time with valid user. username is `ansible` (Change every-time)
5. Then make brute-force on password and password is `pass` (Change every-time)