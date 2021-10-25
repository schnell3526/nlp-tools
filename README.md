# nlp-tools
自然言語処理で利用するツールのDockerfile格納用リポジトリ

## Juman++
[京都大学黒橋研究室](https://nlp.ist.i.kyoto-u.ac.jp/?JUMAN%2B%2B)が開発した形態素解析器
alpine(とにかく軽いイメージを利用したい時)とdebian(Pythonなどもコンテナに導入したい場合)の二つの環境を用意した。マルチステージビルドを利用して極力軽いイメージに仕上げています。

### インストール
```bash
# alpineの場合
docker pull schnell3526/jumanpp:alpine
# debianの場合
docker pull schnell3526/jumanpp:debian
```

### 利用法

ホスト環境で以下のコマンドを実行すれば対話型モードに入れる
```bash
# alpineの場合
docker run -i --rm schnell3526/jumanpp:alpine
# debianの場合
docker run -i --rm schnell3526/jumanpp:debian
```

イメージをローカルに保存していれば次のようにエイリアス登録をすれば実際のjumanppコマンドのように利用できる。
```bash
# alpineの場合
alias jumanpp="docker run -i --rm schnell3526/jumanpp:alpine"
# debianの場合
alias jumanpp="docker run -i --rm schnell3526/jumanpp:debian"
```
このように環境を汚さずにjumanppが導入できます。
```bash
❯ echo 'こんにちは!形態素解析を始めましょう!' | jumanpp
こんにちは こんにちは こんにちは 感動詞 12 * 0 * 0 * 0 "代表表記:こんにちは/こんにちは"
! ! ! 特殊 1 記号 5 * 0 * 0 NIL
形態 けいたい 形態 名詞 6 普通名詞 1 * 0 * 0 "代表表記:形態/けいたい カテゴリ:形・模様"
素 そ 素 名詞 6 普通名詞 1 * 0 * 0 "代表表記:素/そ カテゴリ:抽象物 漢字読み:音"
解析 かいせき 解析 名詞 6 サ変名詞 2 * 0 * 0 "代表表記:解析/かいせき ドメイン:教育・学習;科学・技術 カテゴリ:抽象物"
を を を 助詞 9 格助詞 1 * 0 * 0 NIL
始め はじめ 始める 動詞 2 * 0 母音動詞 1 基本連用形 8 "代表表記:始める/はじめる 反義:動詞:終える/おえる 自他動詞:自:始まる/はじまる 付属動詞候補（基本）"
ましょう ましょう ます 接尾辞 14 動詞性接尾辞 7 動詞性接尾辞ます型 31 意志形 4 "代表表記:ます/ます"
! ! ! 特殊 1 記号 5 * 0 * 0 NIL
EOS
```
