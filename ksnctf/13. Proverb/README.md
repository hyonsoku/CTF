## 問題

## 解放

SSH接続する。実行環境の都合上、`-o IPQoS=none`をつけている。

```zsh
$ ssh q13@ctfq.u1tramarine.blue -p 10013 -o IPQoS=none
```

接続したら、ファイルを見てみる。

```bash
[q13@592fa2a281c1 ~]$ ls -al
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

`proverb`は実行することができる。

```bash
$ ./proverb
The wolf knows what the ill beast thinks.
```

`proverb.txt`も見ることが出来る。

```bash
$ head proverb.txt
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