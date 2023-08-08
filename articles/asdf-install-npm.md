---
title: "asdfを使ってnpmをインストールしてからtextlintを導入する"
emoji: "🐈"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["asdf","npm"]
published: true
---

# はじめに
パソコンを入れ替えたばかりの開発環境が整っていなかったときの対処法メモです。

```fish
Unknown command: npm
```

## asdfを使ってnpmを用意する
昔は、CLIで環境を用意するとき時は[pyenv](https://github.com/pyenv/pyenv)や[rbenv](https://github.com/rbenv/rbenv)を使っていた流れで、[anyenv](https://github.com/anyenv/anyenv)を使っていました。
最近は、[asdf](https://asdf-vm.com/)に落ち着きました。terraformやnpmと広範囲でバージョンを意識しながら導入するのにも便利だったので、今もふと使うのはasdfになります。

npmを使いたいと場合はadsfだと以下となります。

pluginを追加。
```
❯ asdf plugin-add nodejs
```
その後、実行。
```
❯ asdf install nodejs latest
```
なお、バージョンを指定できますが最新は最高なので、latest導入で問題ないです。バージョン指定先を確認するには、`asdf list all nodejs`を使います。

これで、npmが使えるようになりました。と思ったら以下のエラーです。
```
❯ npm -v
No version is set for command npm
Consider adding one of the following versions in your config file at
nodejs 20.5.0
```
そこで、使用するバージョンをきちんと指定します。今回は20.5.0が最新でした。
```
❯ asdf list
nodejs
  20.5.0
❯ asdf local nodejs 20.5.0
❯ asdf list
nodejs
 *20.5.0
```
これで、使えるようになりました。なお、デフォルトが困らないなら`local`を`global`にしてもOKです。

### npmでtextlintを導入して動作確認。
https://zenn.dev/b0b/articles/ga_textlint_proofreading

やりたかったことは上記なので、textlintに必要な設定を導入。
```
❯ npm install textlint --save-dev
```
こちらを筆頭に設定が入りました。

![](/images/articles/textlint_check.jpg)

vscode経由で設定を確認すると、上記のtextlintの指摘が表示されたのでやりたいことはできたようです。
