https://portswigger.net/web-security/authentication/password-based/lab-broken-brute-force-protection-multiple-credentials-per-request

This lab is vulnerable due to a logic flaw in its brute-force protection. To solve the lab, brute-force Carlos's password, then access his account page.

- Victim's username: `carlos`
- [Candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords)

# Lab: Broken brute-force protection, multiple credentials per request

1. First we try to login with invalid username and password. Then we get the massage `Invalid username or password.`
2. We see in burp-suit username and password sending as a json format. we try to send more than 1 password and check there have any error or not.
3. More then one password does not give us any error. so we will write the password at the format to do this we will put the passwords in a file called pass.txt and run this script

```
print("[", end='')

with open("pass.txt", 'r') as f:
    line = f.readlines()

for pwd in line:
    print('"' + pwd.rstrip("\n") + '",' , end='')

print('"random"]', end='')
```

4. Now we put the password and send the request.
5. We got 302. Now we will copy the `Set-Cookie: session=WT8isEKIGHRGspXPIhoFLowWBDVDyFZz;`
6. Now Open inspect go to in `firefox storage` / `chrome aplication` and then cookies and put the value
7. Click My Account and complete the lab.