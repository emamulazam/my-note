https://portswigger.net/web-security/authentication/multi-factor/lab-2fa-bypass-using-a-brute-force-attack

This lab's two-factor authentication is vulnerable to brute-forcing. You have already obtained a valid username and password, but do not have access to the user's 2FA verification code. To solve the lab, brute-force the 2FA code and access Carlos's account page.

Victim's credentials: `carlos:montoya`

# Lab: 2FA bypass using a brute-force attack

1. First we will login by the username and password
2. Here if we give 2 wrong OTP we are logout.
3. Go to settings > sessions > add

![[Authentication Lab 14.png]]

4. In scope include all urls

![[Authentication Lab 14-1.png]]

5. In Details add > run a macro

![[Authentication Lab 14-2.png]]

6. Then select add

![[Authentication Lab 14-3.png]]

7. Select the requests you want

![[Authentication Lab 14-4.png]]

8. If all OK then pick the /login2 request with the request we will send brute force the OTP
9. We will try 0000 to 9999 and we will send the request at a time.
10. When you get status code 302 copy the session code and replace the link in browser.
