## 問題

`exec_me`というファイルをダウンロードできるので、このファイルを実行する。

## 解法

dockerを使ってUbuntuの実行環境を用意する。M1 macの場合、`linux/amd64`を指定しておかないと`amd`

```zsh
$ docker run -it --rm --platform linux/amd64 ubuntu:23.04 /bin/bash
```

`file`コマンドを使いたいので、インストールしておく。

```bash
root@be2c2883bc77:/# apt update && apt upgrade
root@be2c2883bc77:/# apt -y install file wget
```

`wget`を使って、ファイルをダウンロードする。予めブラウザでログインして`cookie`を確認しておき、パラメータに加えた。

```bash
root@be2c2883bc77:/# cd /tmp
root@be2c2883bc77:/tmp# wget --header "cookie: PHPSESSID=XXXXXXXXXXXXXXXXXXXXX" -O exec_me https://ctf.cpaw.site/download.php?param=342992e2fd4444a0d16539bd997b6307
root@be2c2883bc77:/tmp# file exec_me 
exec_me: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 2.6.24, BuildID[sha1]=663a3e0e5a079fddd0de92474688cd6812d3b550, not stripped
```

ファイルの実行権がないので、パーミッションを変更しファイルを実行したらフラグがとれた。

```bash
root@be2c2883bc77:/tmp# ls -l
total 8
-rw-r--r-- 1 root root 4702 Sep 21 15:19 exec_me
root@be2c2883bc77:/tmp# chmod 755 exec_me
root@be2c2883bc77:/tmp# ./exec_me 
cpaw{XXXXXXXXXXXXX}
```