## 問題

ハッシュ値が求められるので、元の値に戻す。

## 解法

### レインボーテーブルのサイト

[Hash Toolkit](https://hashtoolkit.com/)にアクセスして、当該のハッシュ値を入力し、**DECRYPT HASH**をクリック。

Decyptされた文字が表示されるので、フラグの形式`cpaw{}`にして提出。

### CLI

`dcipher-cli`を使ってやってみる。

[k4m4/dcipher-cli: 🔓Crack hashes using online rainbow & lookup table attack services, right from your terminal.](https://github.com/k4m4/dcipher-cli)

dockerを使ってUbuntuの実行環境を用意する。

```zsh
$ docker run -it --rm ubuntu:23.04 /bin/bash
```

`dcipher-cli`をインストールする。

```bash
root@222efb2e0e63:/# cd /tmp
root@222efb2e0e63:/tmp# apt install npm
root@222efb2e0e63:/tmp# npm install -g dcipher-cli
```

あとはコマンドの引数に、ハッシュ値を入れれば、サーチしてくれる。

```bash
root@222efb2e0e63:/tmp# decipher e4c6bced9edff99746401bd077afa92860f83de3
✔ Shal
```