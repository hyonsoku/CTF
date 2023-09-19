8. Basic is secure?

## 問題

`q8.pcap`というファイルが与えられる。

## 解法

pcapファイルなので、Wiresharkを使用して解析する。

macの場合、GUI版をhomebrewを使用してインストールする。

```
brew install --cask wireshark
```

Basic認証としてあたりをつけて、Getメソッドから`Authorization`を見ていると、`credentials`が含まれていたので、それが答え。