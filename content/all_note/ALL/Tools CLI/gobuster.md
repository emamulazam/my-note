
`Gobuster` is a command-line tool used for brut-forcein:

1. **URLs** (directories and files) on web servers
2. **DNS subdomains**
3. **Virtual Hostnames**
4. **Amazon S3 buckets.**

### Common Modes

1. dir -> Brute-force directories/files
2. dns -> Brute-force DNS subdomains
3. vhost -> Brute-force virtual hostnames
4. s3 -> Brute-force S3 buckets

### Directory Brute Forcing (Most Common)

```
gobuster dir -u http://192.168.0.101 -x html,txt,php,js,py -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 100  
```

#### Useful flags

1. `-u` = URL of the target
2. `-w` = Wordlist path
3. `-x` = File extensions (like .php,.html,.txt)
4. `-t` = Number of threads (default is 10)
5. `-o` = Output file to save results
6. `-q` = Quiet mode – only shows found results
7. `--wildcard` = Useful for wildcard response detection
8. `-k` = Skip SSL/TLS certificate verification
9. `-s` = Show only specific status codes (e.g., 200)

### DNS Subdomain Brute Forcing
```
gobuster dns -d example.com -w /usr/share/wordlists/dns/subdomains-top1million-5000.txt
```

**Extra Flags** :
1. `-i` = Show IP addresses of discovered subdomains.
2. `-d` = Domain name.
### VHOST Brute Forcing

```
gobuster vhost -u http://example.com -w /usr/share/wordlists/dns/subdomains-top1million-5000.txt
```
This is used when **name-based** [[virtual hosting]] is suspected.
