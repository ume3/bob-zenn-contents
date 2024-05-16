---
title: "asdfからmise(旧rtx)に乗り換えた話"
emoji: "🏃‍♂️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["asdf","rtx","mise"]
published: true
---

## はじめに

この記事では、私がasdfからmise(旧rtx)に乗り換えた経験について共有します。

[asdfを使っていました](https://zenn.dev/b0b/articles/asdf-install-npm)が、最近の傾向よりrtxが気になっていました。
その[rtxも名前が変わ](https://mise.jdx.dev/rtx.html)って[mise](https://github.com/jdx/mise)になっていたのでmiseの手順として残します。

## 参考
https://minerva.mamansoft.net/Notes/%F0%9F%93%9C2024-01-06+asdf%E3%81%8B%E3%82%89mise%E3%81%AB%E7%A7%BB%E8%A1%8C%E3%81%97%E3%81%A6%E3%81%BF%E3%82%8B

こちらを参考にしました。

## asdfを消す
まず、asdfを使っていましたが思い切って削除します。
ただ、丁寧にやらないといくつかエラーが出るので、手順を確認してから進めます。
一応使っていたバージョンを確認して控えておきます。

```shell
❯ asdf list
golang
 *1.21.4
nodejs
  16.0.0
 *20.5.0
  21.7.1
python
 *3.10.12
  3.11.0
  3.11.4
ruby
 *3.2.2
 ```

まず、これらのプラグインを削除しておきます。
次に、Homebrewで管理しているasdfの削除に移ります。
ちなみに確認したところ依存ライブラリは以下でした。

```shell
❯ brew deps --tree --installed asdf
asdf
├── autoconf
│   └── m4
├── automake
│   └── autoconf
│       └── m4
├── coreutils
│   └── gmp
├── libtool
│   └── m4
├── libyaml
├── openssl@3
│   └── ca-certificates
├── readline
└── unixodbc
    └── libtool
        └── m4
```

[こちらの手順](https://mac.install.guide/faq/uninstall-asdf/)を参考に一気に削除しちゃいます。

```shell
brew uninstall --force asdf
brew autoremove
rm -rf ~/.tool-versions
rm -rf ~/.asdf/
```

asdf経由でインストールしていたnodeなどのエラーが出た場合はターミナルのシェルを再読み込みするとよいでしょう。
ここまでやや強制的に削除しましたが、順を追うなら丁寧に1つずつ消したほうがよさそうです。ただ、これでいったんasdfの環境を削除しました。

## miseを入れる
次に、miseをインストールする手順について説明します。これは公式のとおりですね。
その上でHomebrewを使ってインストールします。

```shell
> brew install mise
```

```
Error: usage CLI not found. This is required for completions to work in mise.
See https://usage.jdx.dev for more information.
```

なお、私の環境ではプロンプトに以下のエラーがでたので、`usage`を導入して回避できました。

```shell
❯ brew install usage
```

### miseのplugin経由でnodeのインストール
miseを使ってnpmをインストールする方法について説明します。

```shell
❯ mise use --global node@latest
mise node@22.2.0 ✓ installed                                                                        mise ~/.config/mise/config.toml tools: node@22.2.0
```

これで最新版はインストールされます。
あとは、pythonとかrubyやGoなど必要に応じてバージョンも指定できます。

複数バージョン入れる場合は同様に。都度切り替えればOKです。
```shell
❯ mise use --global node@16.0.0
mise node@16.0.0 ✓ installed                                                                        mise ~/.config/mise/config.toml tools: node@16.0.0

❯ mise list
Plugin  Version  Config Source              Requested
go      1.22.3   ~/.config/mise/config.toml latest
node    16.0.0   ~/.config/mise/config.toml 16.0.0
node    22.2.0

❯ mise use --global node
mise ~/.config/mise/config.toml tools: node@22.2.0

❯ mise list
Plugin  Version  Config Source              Requested
go      1.22.3   ~/.config/mise/config.toml latest
node    16.0.0
node    22.2.0   ~/.config/mise/config.toml latest

❯ cat ~/.mise.toml
[tools]
node = "latest"
```

`asdf local`のような設定はありませんが、ディレクトリごとにバージョンを切り替えることができます。さきほどの例はglobalを指定しないことでローカルに反映されています。上記は、該当ディレクトリでの実行なので、移動すれば別バージョンのデフォルト設定が機能します。

なお、miseには[direnvと同等の機能](https://mise.jdx.dev/direnv.html)があります。

### mise configについて

miseのhelpより今後用意される機能についても紹介します。

```shell
###   config       [experimental] Manage config files [aliases: cfg]
❯ mise config ls
mise `mise config ls` is experimental. Enable it with `mise settings set experimental true`
mise Run with --verbose or MISE_VERBOSE=1 for more information

❯ mise version
2024.5.16 macos-arm64 (2024-05-15)
```

この設定は今使ってるバージョンではデフォルトで設定されていません（experimental）が、設定することで以下のように扱えます。

```
❯ mise settings set experimental true
❯ mise config ls
Path                       Plugins
~/.mise.toml               node
~/.config/mise/config.toml node, go

❯ cat  ~/.config/mise/config.toml
[tools]
node = "latest"
go = "latest"

[settings]
experimental = true
```

これで、プロジェクトごとにバージョンを切り替えた際に、どのバージョンが設定されているか確認できます。


## おわりに

miseへの乗り換えは私にとって大きな変化でしたが、新しい環境に慣れるまでの努力は報われました。今ではmiseを使うことで、より効率的な開発環境が整いました。plugin-addの初期設定がないだけでもお手軽に感じますし、将来の木の追加にも期待しています。

この記事が他の方々の乗り換えの参考になれば幸いです。