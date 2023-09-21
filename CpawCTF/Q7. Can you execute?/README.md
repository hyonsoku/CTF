## 問題

`exec_me`というファイルをダウンロードできるので、このファイルを実行する。

## 解法

dockerを使ってUbuntuの実行環境を用意する。

```zsh
$ docker run -it --rm ubuntu:23.04 /bin/bash
```

`file`コマンドを使いたいので、インストールしておく。

```bash
root@3939c56c64ba:/# apt update
root@3939c56c64ba:/# apt upgrade
root@3939c56c64ba:/# apt install file
```