---
title: "VS code+textlint+Zennの執筆環境を整えてみた"
emoji: "🐙"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["zenn","vscode","textlint"]
published: true
published_at: 2023-05-08 10:00
---

## はじめに
textlint+reviewdog環境を用意してみました。今度は、vscodeを使った執筆環境にしたかったので、vscode-textlintとZennのpluginを導入しました。その環境設定をまとめた記事になります。

### 参考記事
- [ZennのVSCode Web拡張\(β版\)をリリースしました \| What's New in Zenn](https://info.zenn.dev/release-vscode-extension)
- [vscode\-textlint \- Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=taichi.vscode-textlint)
- [textlint と VS Code で始める文章校正 \- Qiita](https://qiita.com/takasp/items/22f7f72b691fda30aea2)

### VS Code + Zenn
VS Code(Visual Studio Code)の操作や導入は省略しますが、手軽に試すならvscode.devがあります。

https://vscode.dev/

また、[GitHubとZennが連携していれば](https://zenn.dev/zenn/articles/usage-github-dev)、自分のリポジトリ内で`.`のショートカットを実行するか、`github.com -> github.dev`に変更するだけでVS Codeのエディタを開くことができます。

まずはZennの拡張機能ことMarketplaceからZennのpluginを導入します。するとサイドバーにZennのアイコンが表示されますのでクリックすると、Zennを考慮したエディタとして使うことができるようになります。

![](/images/articles/vscode_zenn_preview.jpg)

参考記事を元に執筆しながらプレビューできる点がメリットです。zenn-cliでやっていた`npx zenn preview`と同様の機能を手軽に使うことができるようになりました。

### VS Code + textlint
今度は、参考記事を元にtextlintの拡張機能を同様にインストールします。

![](/images/articles/vscode_texlint.jpg)

上記のように、リアルタイムにtextlintのチェックが入るので、Pull requests前に気づけることができて便利です。

### おわりに
これで、VS Codeを使う際にZennに特化した執筆環境を整えることができました。この記事もVS Code上で書いていますが、textlintが自動的に働いて文書をチェックしてくれるので便利です。これで、だいぶ効率化された環境で文章を書くことができるようになりました。