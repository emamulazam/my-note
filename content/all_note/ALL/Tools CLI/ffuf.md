
The `ffuf` (Fuzz Faster U Fool) tool is a fast and powerful web fuzzer written in Go, commonly used in web penetration testing and bug bounty hunting

## Directory Bruteforcing

```
ffuf -u https://site.com/FUZZ -w common.txt -fc 404
```

## Login Parameter Fuzzing

```
ffuf -u https://site.com/login -X POST -d "user=admin&pass=FUZZ" -w passwords.txt -mc 200
```

## Virtual Host Discovery

```
ffuf -u http://TARGET -H "Host: FUZZ.target.com" -w subdomains.txt
```

## Subdomain Fuzzing with DNS

```
ffuf -u http://FUZZ.target.com -w subdomains.txt -H "Host: FUZZ.target.com" -fs 0
```


## Useful Flags

### 1. **-u (URL)**

Specifies the URL with the `FUZZ` keyword.
```
-u https://example.com/FUZZ
```

### 2. **-w (Wordlist)**

Path to the wordlist.
```
-w /usr/share/wordlists/dirb/common.txt
```

#### 3. **-t (Threads)**

Number of concurrent threads (faster but heavier).
```
-t 50
```

### 4. **-mc (Match Code)**

Only show responses with specific HTTP status codes.
```
-mc 200,403
```

### 5. **-fc (Filter Code)**

Filter out responses with specific HTTP status codes.
```
-fc 404
```

### 6. **-o (Output)**

Save results to a file.
```
-o result.json -of json
```

### 7. **-recursion & -recursion-depth**

Useful for recursive directory fuzzing.
```
-recursion -recursion-depth 2
```

### 8. **-H (Header)**

Add custom headers (e.g., for cookies or tokens).
```
-H "Authorization: Bearer TOKEN"
```


#### 9. **-X (HTTP Method)**

Change HTTP method (e.g., POST, PUT).
```
-X POST
```

#### 10. **-d (Data)**

Send POST data.
```
-d "username=admin&password=FUZZ"
```

### 11. **-fs (Filter by Response Size)**

Don't Show 1556 byte size file if the input is
```
-fs 1556
```

