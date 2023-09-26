CTFで使うようのdockerコンテナ

## 使い方

1. Dockerfileを作成

2. イメージをビルドする

```bash
> docker build --tag ctf:1.1 .
```

3. コンテナイメージを実行する

```bash
> docker run -it --rm --volume $(pwd):/home/hyonsoku ctf:1.1 /bin/bash
```