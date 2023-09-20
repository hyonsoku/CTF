## 問題

sshコマンドと、パスワードが教えられる。

```
ssh q13@ctfq.u1tramarine.blue -p 10013
Password: 8zvWx00MakSCQuGq
```

## 解法

SSH接続する。実行環境の都合上、`-o IPQoS=none`をつけている。

```zsh
$ ssh q13@ctfq.u1tramarine.blue -p 10013 -o IPQoS=none
```

接続したら、ファイルを見てみる。

```bash
[q13@545d4e166111 ~]$ ls -al
total 52
dr-xr-xr-x 1 root root  4096 Feb 25  2021 .
drwxr-xr-x 1 root root  4096 Feb 25  2021 ..
-rw-r--r-- 1 q13  q13     18 Jul 21  2020 .bash_logout
-rw-r--r-- 1 q13  q13    141 Jul 21  2020 .bash_profile
-rw-r--r-- 1 q13  q13    543 Feb 25  2021 .bashrc
-r-------- 1 q13a q13a    22 Feb 25  2021 flag.txt
---s--x--x 1 q13a q13a 24144 Feb 25  2021 proverb
-r--r--r-- 1 q13a q13a   755 Feb 25  2021 proverb.txt
```

`flag.txt`というテキストファイルが怪しいが、ownerがq13aとなっていて、開くことができない。

`proverb`は実行することができる。アクセス権についている`s`は、setuid bitと呼ばれるもので、ファイル所有者の権限で実行できる。

```bash
[q13@545d4e166111 ~]$ ./proverb
The wolf knows what the ill beast thinks.
```

`proverb.txt`も見ることが出来る。

```bash
[q13@545d4e166111 ~]$ head proverb.txt
All's well that ends well.
A good beginning makes a good ending.
Many a true word is spoken in jest.
Fear is often greater than the danger.
Go for broke!
Fire is a good servant but a bad master.
The wolf knows what the ill beast thinks.
There is always a next time.
Spare the rod and spoil the child.
The calm before the storm.
```

`proverb`の実行結果が、`proverb.txt`内の文字列と一致しているので、`proverb.txt`を読み込んで表示させていると予想。

Symlink Attackを検討する。どこか、シンボリックリンクを張れそうなところを探すと、`/tmp/`に書き込み権限がある。

```bash
[q13@545d4e166111 ~]$ ll /
total 64
drwxr-xr-x   1 root root 4096 Sep 20 04:26 ./
drwxr-xr-x   1 root root 4096 Sep 20 04:26 ../
-rwxr-xr-x   1 root root    0 Sep 20 04:26 .dockerenv*
lrwxrwxrwx   1 root root    7 Nov  3  2020 bin -> usr/bin/
drwxr-xr-x   5 root root  340 Sep 20 04:26 dev/
drwxr-xr-x   1 root root 4096 Sep 20 04:26 etc/
drwxr-xr-x   1 root root 4096 Feb 25  2021 home/
lrwxrwxrwx   1 root root    7 Nov  3  2020 lib -> usr/lib/
lrwxrwxrwx   1 root root    9 Nov  3  2020 lib64 -> usr/lib64/
drwx------   2 root root 4096 Dec  4  2020 lost+found/
drwxr-xr-x   2 root root 4096 Nov  3  2020 media/
drwxr-xr-x   2 root root 4096 Nov  3  2020 mnt/
drwxr-xr-x   2 root root 4096 Nov  3  2020 opt/
dr-xr-xr-x 231 root root    0 Sep 20 04:26 proc/
dr-xr-x---   2 root root 4096 Dec  4  2020 root/
drwxr-xr-x   1 root root 4096 Sep 20 04:26 run/
lrwxrwxrwx   1 root root    8 Nov  3  2020 sbin -> usr/sbin/
drwxr-xr-x   2 root root 4096 Nov  3  2020 srv/
dr-xr-xr-x  13 root root    0 Sep 20 04:26 sys/
drwxrwxrwt   1 root root 4096 Feb 25  2021 tmp/
drwxr-xr-x   1 root root 4096 Dec  4  2020 usr/
drwxr-xr-x   1 root root 4096 Dec  4  2020 var/
```

シンボリックリンクを張った側のproverbを実行すると、`proverb.txt`を開けないとなるので、やはり当該ファイルを読み込んでいる様子。

```bash
[q13@545d4e166111 ~]$ cd /tmp
[q13@545d4e166111 tmp]$ ln -s /home/q13/proverb ./proverb
[q13@545d4e166111 tmp]$ ./proverb 
Failed to open proverb.txt
```

同様にして、`flag.txt`もファイル名を`proverb.txt`に変更してシンボリックリンクを張る。

```bash
[q13@e1c3f1fe0bfb tmp]$ ln -s ~/flag.txt ./proveb.txt
```

```bash
[q13@e1c3f1fe0bfb tmp]$ ll
total 36
drwxrwxrwt 1 root root 4096 Feb 25  2021 ./
drwxr-xr-x 1 root root 4096 Sep 20 04:42 ../
drwxrwxrwt 2 root root 4096 Dec  4  2020 .ICE-unix/
drwxrwxrwt 2 root root 4096 Dec  4  2020 .Test-unix/
drwxrwxrwt 2 root root 4096 Dec  4  2020 .X11-unix/
drwxrwxrwt 2 root root 4096 Dec  4  2020 .XIM-unix/
drwxrwxrwt 2 root root 4096 Dec  4  2020 .font-unix/
-rwx------ 1 root root  701 Dec  4  2020 ks-script-esd4my7v*
-rwx------ 1 root root  671 Dec  4  2020 ks-script-eusq_sc5*
lrwxrwxrwx 1 q13  q13    17 Sep 20 04:48 proverb -> /home/q13/proverb*
lrwxrwxrwx 1 q13  q13    18 Sep 20 04:48 proverb.txt -> /home/q13/flag.txt
```

`proverb`を実行してみるが、`proverb.txt`を開けないと怒られる。

```bash
[q13@e1c3f1fe0bfb tmp]$ ./proverb 
Failed to open proverb.txt
```