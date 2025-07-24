https://portswigger.net/web-security/authentication/multi-factor/lab-2fa-simple-bypass

This lab's two-factor authentication can be bypassed. You have already obtained a valid username and password, but do not have access to the user's 2FA verification code. To solve the lab, access Carlos's account page.

- Your credentials: `wiener:peter`
- Victim's credentials `carlos:montoya`

# Lab: 2FA simple bypass

1. First login with your credentials.
2. Then click `Email Client` and put the OTP.
3. Now logout and try to login with Victim's credentials.
4. Now replace `/login2` with `/my-account` and solve the lab.