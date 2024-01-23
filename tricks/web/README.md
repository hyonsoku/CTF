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

### Python

`open`はスラッシュ`/`がいくつあってもよい。

```python
f = open("./etc/flag", "rb")
f = open("./etc/////flag", "rb")
```

# tools

- [HTTPie](https://httpie.io/)
- [HTTP Prompt](https://http-prompt.com/)