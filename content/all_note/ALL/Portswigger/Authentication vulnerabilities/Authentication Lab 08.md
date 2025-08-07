https://portswigger.net/web-security/authentication/multi-factor/lab-2fa-broken-logic

This lab's two-factor authentication is vulnerable due to its flawed logic. To solve the lab, access Carlos's account page.

- Your credentials: `wiener:peter`
- Victim's username: `carlos`

You also have access to the email server to receive your 2FA verification code.

# Lab: 2FA broken logic

1. Login with your credentials. And the email you get.
2. see the `/login` and `/login2` request in burp-suit.
3. In `/login2` remove `session` and send the request. And get no change.
4. First do with without correct sign and then with correct sign.
5. Replace `verify=wiener` with `verify=carlos` and send the request and do it 4-5 time to check brute-force protection have or not.
6. There have not any brute-force protection in the otp section so we will brute-force `mfa-code=0533` this otp.
7. We will use Brute forcer, character set 0 to 9 and length 4.
8. We will wait for some time then we will find the right OTP and the status code will 302.
9. Then click right button and click show response in browser.
10. And solve the lab.