---
title: "textlint+reviewdogでGitHub Actionsでの文書校正を楽々実現！vscodeも添えて"
emoji: "⤴️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["textlint","reviewdog"]
published: false
---

## はじめに
textlintを導入して校正ができるようになりました。これは、Zennで記事を書くときに校正をしたいからです。ただ、今の状況だとtextlintを都度実行することで実現しています。せっかくGitHubとZennを連携したので、これを、PullRequestのタイミングでtextlintを実行すべくGitHubActionsに取り入れることにしました。

また、vscodeを使った執筆をしたかったのでvscode-textlintも導入。Zennのpluginもあることが知れたので、このあたりの環境設定をまとめることにしました。

### 参考記事
- [zenn\-cli \+ reviewdog \+ textlint \+ GitHub Actions で執筆体験を最高にする](https://zenn.dev/serima/articles/4dac7baf0b9377b0b58b#%E7%95%AA%E5%A4%96%E7%B7%A8%3A-vscode-textlint)
- [textlint と VS Code で始める文章校正 \- Qiita](https://qiita.com/takasp/items/22f7f72b691fda30aea2)
- [GitHub ActionsでZennブログの校正を自動化してみた](https://zenn.dev/yuta28/articles/blog-lint-ci-reviewdog)

### textlint + reviewdog
わざとここでまちがえてみ,る


### vscode + textlint + zenn