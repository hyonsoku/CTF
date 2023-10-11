## 問題

>フラグを出す実行ファイルがあるのだが、プログラム(elfファイル)作成者が出力する関数を書き忘れてしまったらしい…
> reverse100

## 解法

まずは、ファイルをダウンロードして、`file`コマンドを実行して様子を見る。

```bash
$ wget --header "cookie: PHPSESSID=vsge452av959ulna6kc3rl0sq3" -O reverse100 https://ctf.cpaw.site/download.php?param=ee353729ac18b851cb3db3371945dd62
$ file reverse100 
reverse100: ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, for GNU/Linux 2.6.24, BuildID[sha1]=f94360edd84a940de2b74007d4289705601d618d, not stripped
```

ファイル内にフラグが埋め込まれていると予測し、`strings`を実行してみる。

```bash
$ strings reverse100
（前略）
D$Fcpawf
D$J{
D$ y
D$$a
D$(k
D$,i
D$0n
D$4i
D$8k
D$<u
D$@!
（後略）
```

`capw`の後に、フラグっぽい文字列が見えたので、フォーマットを整えて提出。