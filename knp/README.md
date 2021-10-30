# knp

[京都大学黒橋研究室](https://nlp.ist.i.kyoto-u.ac.jp/?KNP)が開発した日本語文の構文・格・照応解析を行うシステム。
debian環境でのDockerfileを用意した。マルチステージビルドを利用して極力軽いイメージに仕上げています。

## インストール

- Docker Hubからpullする場合

```bash
docker pull schnell3526/knp:debian
```

- ローカルでビルドする場合

```bash
git clone https://github.com/schnell3526/nlp-tools.git
cd knp/debian
docker build --tag schnell3526/knp:debian .
```

## 利用法

ホスト環境で以下のコマンドを実行すれば対話型モードに入れる

```bash
docker run -i --rm schnell3526/knp:debian
```

jumanppの解析結果を食わせて使う。
