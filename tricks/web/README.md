# HTTP

## HTTP Header

- `Referer`
参照元のURLを偽装できる。

[Referer - HTTP | MDN](https://developer.mozilla.org/ja/docs/Web/HTTP/Headers/Referer)

- `Referrer`

一部のwebアプリ(express 4.x等)では、`Referrer`を`Referer`として解釈してくれる。
これにより、`Referer`と組み合わせることで、二つの値を送信することができる。

# パストラバーサル

## フィルターのバイパス

### URLエンコーディング

特別な文字をURLに含めたいときに、`%`と対応する2文字の16進数に置き換える。

デコードされた文字列がフィルターに引っかからないよう`%`自体を`%25`に置き換えるダブルエンコーディングもある。

| Character | ASCII | Encode | Double Encoding |
|-----------|-------|--------|-----------------|
| space     |       | `%20`  | `%2520`         |
| `%`       |       | `%25`  | `%2525`         |
| `+`       |       | `%2B`  | `%252B`         |
| `.`       |       | `%2E`  | `%252E`         |
| `/`       |       | `%2F`  | `%252F`         |
| `<`       |       | `%3C`  | `%253C`         |
| `=`       |       | `%3D`  | `%253D`         |
| `>`       |       | `%3E`  | `%253E`         |
| `\`       |       | `%5C`  | `%255C`         |

[HTML URL Encoding Reference](https://www.w3schools.com/tags/ref_urlencode.ASP)

### Python

`open`はスラッシュ`/`がいくつあってもよい。

```python
f = open("./etc/flag", "rb")
f = open("./etc/////flag", "rb")
```

# tools

- [HTTPie](https://httpie.io/)
- [HTTP Prompt](https://http-prompt.com/)