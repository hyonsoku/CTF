## 問題

与えらえたURLにアクセスすると、時刻のようなものが表示される。

![Image 1](ksnctf_q12_1.jpg)

## 解法

リロードすると、値が変わる。

![Image 2](ksnctf_q12_2.jpg)

`2012:1823`で検索すると、`CVE-2012-1823`というPHPの脆弱性がヒットする。PHPのバージョンが、5.3.12以前もしくは、5.4.2以前で影響がある模様。

[CVE Record | CVE](https://www.cve.org/CVERecord?id=CVE-2012-1823)

`curl`でレスポンスヘッダーを見ると、PHP 5.4.1が使われていそうなので、この脆弱性を利用したい。

```bash
$ curl https://ctfq.u1tramarine.blue/q12/ -i
HTTP/2 200 
server: nginx
date: Tue, 19 Sep 2023 12:16:42 GMT
content-type: text/html
x-powered-by: PHP/5.4.1
```

脆弱性対策データベースによると、

> PHP には、CGI として使用される設定において query string をコマンドラインオプションとして認識してしまう脆弱性が存在します。

だそうです。

[JVNDB-2012-002235 - JVN iPedia - 脆弱性対策情報データベース](https://jvndb.jvn.jp/ja/contents/2012/JVNDB-2012-002235.html)

PHPのコマンドラインオプションは、[PHP: オプション - Manual](https://www.php.net/manual/ja/features.commandline.options.php)から、
調べることが、できる。

試しにソースコードを出力する`-s`オプションをurlにつけた、`https://ctfq.u1tramarine.blue/q12/?-s`でアクセスしてみると、
ソースコードが開示された。

```php
<?php

    //  Flag is in this directory.

    date_default_timezone_set('UTC');
    
    $t = '2012:1823:20:';
    $t .= date('y:m:d:H:i:s');
    for($i=0;$i<4;$i++)
        $t .= sprintf(':%02d',mt_rand(0,59));
?>
（以下、省略）
```

どうやら、このソースコードがあるディレクトリにFLAGがある様子。

指定したPHPのコードが実行できるようなので、OSコマンドインジェクションを実行する。

[CAPEC - CAPEC-88: OS Command Injection (Version 3.9)](https://capec.mitre.org/data/definitions/88.html)

PHPからOSのコマンドを実行する方法を調べて見ると、`exec()`, `system()`, `passthru()`, `shell_exec()`, `pcntl_exec()`あたりがヒットするので、これらのコマンドを使えないか検討する。