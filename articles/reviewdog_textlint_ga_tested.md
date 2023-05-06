---
title: "textlint+reviewdogでGitHub Actionsでの文書校正を楽々実現！"
emoji: "⤴️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["textlint","reviewdog"]
published: true
published_at: 2023-05-07 10:00
---

# はじめに
[textlintを導入して校正](https://zenn.dev/b0b/articles/ga_textlint_proofreading)ができるようになりました。これは、Zennで記事を書くときに校正を目的としています。ただ、今の状況だとtextlintを都度実行する必要があります。せっかくGitHubとZennを連携したので、これを、PullRequestのタイミングでtextlintを実行すべくGitHubActionsに取り入れることにしました。

## 参考記事
- [zenn\-cli \+ reviewdog \+ textlint \+ GitHub Actions で執筆体験を最高にする](https://zenn.dev/serima/articles/4dac7baf0b9377b0b58b#%E7%95%AA%E5%A4%96%E7%B7%A8%3A-vscode-textlint)
- [GitHub ActionsでZennブログの校正を自動化してみた](https://zenn.dev/yuta28/articles/blog-lint-ci-reviewdog)

## textlint+reviewdogのworkflow
textlintのGitHub Actionsに[reviewdogを想定したworkflowのサンプル](https://github.com/marketplace/actions/run-textlint-with-reviewdog#githubworkflowsreviewdogyml)が用意されています。これを使います。

https://github.com/ume3/bob-zenn-contents/blob/d025a48c4287e9c2bc47e61c23f1bb2c483be52b/.github/workflows/reviewdog.yml#L32-L38

ポイントは`github_token`をPATにしている点です。いろいろやり方はあると思いますが、こちらを採用しました。参考記事だと、`github_token: ${{ secrets.GITHUB_TOKEN }}`とするパターンが多かったのですが、今回は権限が足りていと判断しました。

```
 Running textlint with reviewdog 🐶 ...
    (省略)
  403 Resource not accessible by integration []
```

### Pull Requestに必要なworkflowの権限設定
personal access tokens (classic) であれば、以下を付与したPATを用意すれば動きそうです。

- repo
- repo:status
- pull_request

ただ、せっかく[Fine-grained personal access tokensを試した](https://zenn.dev/b0b/articles/fine-grained-pat-usageb)ので、こちらで権限を設定してみることにします。この場合は以下となります。

![](/images/articles/pat_zenn_only.jpg)

- Contents .. repo
- Coomit statuses ... repo:status
- Pull requests ... pull_request

それぞれはclassic設定のこちらにあてはまると判断して設定。あとは、GitHubのリポジトリのページに移動して、「Settings」-「Secrets」-「New repository secret」をクリックし、トークン名と値を入力して保存すれば使えるようになります。

### reviewdogの動作確認
試しにtextlintでひっかかりそうな文章を書いて、Pull requestsを実施。まずはworkflowの動作を確認。

![](/images/articles/reviewdog_run.jpg)

その後、コメントで以下のようにreviewdogが校正チェックをしてくれました。

![](/images/articles/miss-reviewdog.jpg)

> あとはコメントに沿って指摘事項を取り入れるか判断することができる状態になりました。

上記のように、わざと間違えてみたところ以下のレビューが入りました。

https://github.com/ume3/bob-zenn-contents/pull/10#discussion_r1186645237

fixすることで修正をとりいれることもできます。

# おわりに
参考記事を読んでもはまたっところは、nodeが使い慣れていなくてpackage.json用意で躓いた点と、PATの権限の付与と設定ぐらいでした。
textlint+reviewdogのworkflow用意は簡単ながら効果が大きいのでこの設定で様子見しつつ執筆していきたいです。