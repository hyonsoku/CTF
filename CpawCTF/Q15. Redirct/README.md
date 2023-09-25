## 問題

> このURLにアクセスすると、他のページにリダイレクトされてしまうらしい。
> 果たしてリダイレクトはどのようにされているのだろうか…
> http://q15.ctf.cpaw.site

## 解法

何が起きているか確認するために、`curl`コマンドを実行する。

`--head`オプションで、レスポンスヘッダーを確認する。

```bash
$ curl --head http://q15.ctf.cpaw.site/
HTTP/1.1 302 Found
Server: nginx
Date: Mon, 25 Sep 2023 11:53:22 GMT
Content-Type: text/html; charset=UTF-8
Connection: keep-alive
X-Flag: cpaw{4re_y0u_1ook1ng_http_h3ader?}
Location: http://q9.ctf.cpaw.site
```

ヘッダーを見ると、フラグが隠されていた。