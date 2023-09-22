## 問題

> このファイルを開きたいが拡張子がないので、どのような種類のファイルで、どのアプリケーションで開けば良いかわからない。
> どうにかして、この拡張子がないこのファイルの種類を特定し、どのアプリケーションで開くか調べてくれ。
> 問題ファイル： open_me

## 解法

Q7と同じく、とりあえずダウンロードして`file`コマンドで調査する。

```zsh
$ docker run -it --rm --platform linux/amd64 ubuntu:23.04 /bin/bash
```

```bash
root@77319bec93ef:/# apt update && apt upgrade
root@77319bec93ef:/# apt -y install file wget
root@77319bec93ef:/# wget --header "cookie: PHPSESSID=tu0tt1fvth226fi8gvg4mb4k66" -O open_me https://ctf.cpaw.site/download.php?param=e44b3198036df7fb047516035ec989e1
root@77319bec93ef:/# file open_me 
open_me: Composite Document File V2 Document, Little Endian, Os: Windows, Version 10.0, Code page: 932, Author: v, Template: Normal.dotm, Last Saved By: v, Revision Number: 1, Name of Creating Application: Microsoft Office Word, Total Editing Time: 28:00, Create Time/Date: Mon Oct 12 04:27:00 2015, Last Saved Time/Date: Mon Oct 12 04:55:00 2015, Number of Pages: 1, Number of Words: 3, Number of Characters: 23, Security: 0
```

Microsoft Office Wordのファイルだということが分かったので、そのままWordで開いてみたらフラッグが表示された。