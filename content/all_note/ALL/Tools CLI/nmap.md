
Nmap is `a free and open-source utility used for network exploration and security auditing`

### Basic

Think ip = 192.168.0.101 
Basic command for nmap:

```
nmap 192.168.0.101
```
Scan top 1000 ports

```
nmap -vvv 192.168.0.101
```
print only open ports

```
nmap -T5 -A -Pn -sC -p21,22,80,445 192.168.0.101
```
`-T5` = Fastest scan
`-A` = Enable OS detection, version detection, script scanning, and traceroute
`-p` = Port number what should scan
`-Pn` = Scan ports without ping
`-sC` = default script

### Some useful flags

1.  `-iL` = Input from list of hosts/networks
2.  `-sS` = TCP SYN
3.  `-p` = Port number what should scan
4.  `-sV` = Open port service/version info
5.  `-sC` = equivalent to --script=default
6.  `-O` = Enable OS detection
7.  `-oN` = Output file in `.txt` format
8.  `-v` = Increase verbosity level (use `-vv `or more for greater effect)
9.  `-A` = Enable OS detection, version detection, script scanning, and trace-route
