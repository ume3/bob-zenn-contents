---
title: "Zenn CLIで初めて記事を書いてみた(2023年5月版)"
emoji: "🎁"
type: "idea"
topics: [zenn]
published: true
---

## はじめに
Zennをはじめようとなりました。Zenn CLIが便利らしいとのことで、こちらを利用した記録となります。GitHub連携が必須の設定となりますが、こちらのほうが管理しやすいと判断しました。

そこで、つまずきどころと感想をまとめてみました。

### 環境想定
- Mac(M1)
- CLI（ターミナル操作前提）
  - この記事もvimで執筆

### 参考記事
ここを読めばやりたいことはほぼできます。

- [Zenn CLIで記事・本を管理する方法](https://zenn.dev/zenn/articles/zenn-cli-guide)
- [GitHubリポジトリでZennのコンテンツを管理する](https://zenn.dev/zenn/articles/connect-to-github)
- [ZennとGithubを連携する方法](https://zenn.dev/eguchi244_dev/articles/github-zenn-linkage-20230501#github%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%97%E3%81%A6%E8%A8%98%E4%BA%8B%E3%82%92%E4%BD%9C%E6%88%90%E3%81%99%E3%82%8B)

### やってみたこと

#### Zenn CLIインストールとコマンド操作
[Zenn CLIをインストールする](https://zenn.dev/zenn/articles/install-zenn-cli#zenn-cli%E3%81%AE%E5%B0%8E%E5%85%A5%E6%89%8B%E9%A0%86)

まず公式に沿ってインストールしましたが、とくに問題なかったです。

```
❯ npx zenn init

  🎉  Done!
  早速コンテンツを作成しましょう

  👇  新しい記事を作成する
  $ zenn new:article

  👇  新しい本を作成する
  $ zenn new:book

  👇  投稿をプレビューする
  $ zenn preview
```

[Zenn CLIで記事・本を管理する方法](https://zenn.dev/zenn/articles/zenn-cli-guide)

記事の作成は、URL生成名に関係するので[slug（スラッグ）](https://zenn.dev/zenn/articles/what-is-slug)を意識するとよさそうです。

```
❯ npx zenn new:article --slug zenn_cli_test_20230504
created: articles/zenn_cli_test_20230504.md
```

たとえばこの記事は上記のコマンドでslugを指定して生成しました。注意点は名前がかぶってはダメです。

#### 生成された記事の扱い方
サンプルの記事の中身より、いくつか設定箇所があります。

- <emoji> ... 好きな絵文字を入れると、タイトルに表記。見栄えが良い。
- <type> ... tech or ideaでよさそうです。[詳細はこちら](https://zenn.dev/tech-or-idea)。
- <topics> ... トピック一覧に掲載されます。[zennとすると、このようにカテゴライズ](https://zenn.dev/topics/zenn)されます。

はじめて書くときは、こちらの[Zennの公式のページ(今回は一例）](https://github.com/zenn-dev/zenn-docs/blob/main/articles/zenn-cli-guide.md)を見るとよいとマニュアルでも補足がありました。

あとは、公開設定のON/OFFとなる、[published]の設定をすればOK。公開タイミングも調整できるようです。

#### 編集時のプレビュー機能
```
❯ npx zenn preview
👀 Preview: http://localhost:8000
```
ブラウザでアクセスすると、以下のような表示となります。

![](/images/articles/zenn_editor_preview.jpg)

なお、この画像は、[GUIでのアップロード](https://zenn.dev/dashboard/uploader)を試したところお手軽ですが管理しづらいと判断。[リポジトリ内管理](https://zenn.dev/zenn/articles/deploy-github-images)を採用しました。

### おわりに
あとはここまでの記事を書いてまとめてテストアップロードとしてみて終わりです。

簡単でお手軽ですね！むしろ、GitHubのToken設定の新しい機能(Fine-grained personal access tokens (beta))を試したときにはまったぐらいです。よって、ハマるポイントはほぼないぐらいにマニュアルが整備されていてすごいなという感想でした。次は、Bookにチャレンジしたいと思います。
