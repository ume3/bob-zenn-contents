---
title: "textlintで校正する"
emoji: "📝"
type: "tech"
topics: [textlint]
published: true
published_at: 2023-05-05 10:00
---

## はじめに
[Zenn CLIで記事を書いてみました](https://zenn.dev/b0b/articles/zenn_cli_test_20230504)。せっかくGitHub経由で記事を書くので、校正をしながら文書を書きたいところです。

### 参考記事
- [GitHub ActionsでZennブログの校正を自動化してみた](https://zenn.dev/yuta28/articles/blog-lint-ci-reviewdog)

### やったこと
校正と言えば、textlintですね。

まずはtextlintをインストールして、実際に活用してみました。自動校正は次の機会にやります。

#### textlintのルールセットのインストール
いろんなルールセットがあるので、参考記事をみながら必要そうなものをインストールしました。

```
# そもそもtextlintの導入
# https://github.com/textlint/textlint
npm install textlint --save-dev

# 技術書向けのルールセット
# https://github.com/textlint-ja/textlint-rule-preset-ja-technical-writing
npm install textlint-rule-preset-ja-technical-writing

# SmartHRさん公開のルールセット
# https://github.com/kufu/textlint-rule-preset-smarthr
npm install textlint-rule-preset-smarthr

# ルールのパス指定
# https://github.com/textlint-rule/textlint-rule-prh
npm install textlint-rule-prh

# 許可リスト設定
# https://github.com/textlint/textlint-filter-rule-allowlist
npm install textlint-filter-rule-allowlist
```

以下の設定を用意したことになります。
```
❯ npm ls | grep textlint | awk -F@ '{print $1}' | sort
├── textlint
├── textlint-filter-rule-allowlist
├── textlint-rule-preset-ja-technical-writing
├── textlint-rule-preset-smarthr
├── textlint-rule-prh
```
#### textlintの動作確認
textlintが働いているかはruleを指定すると以下の動きをみることができます。

```
❯ npx textlint --preset ja-technical-writing articles/zenn_cli_test_20230504.md

/Users/<省略>/articles/zenn_cli_test_20230504.md

You should close this sentence with ）.
This pair mark is called 丸括弧（）                   ja-technical-writing/no-unmatched-pair
  67:121  error  一文に二回以上利用されている助詞 "と" がみつかりました。  ja-technical-writing/no-doubled-joshi
  85:10   error  Disallow to use "！"                                      ja-technical-writing/no-exclamation-question-mark
  85:159  error  弱い表現: "思います" が使われています。                   ja-technical-writing/ja-no-weak-phrase

✖ 3 problems (3 errors, 0 warnings)
```

試しに適当なMarkDownファイルに適用してみたところ、上記の指摘が入りました。必要に応じて修正します。

#### .textlintrcの設定
参考記事をベースに用意したファイルは以下となります。

https://github.com/ume3/bob-zenn-contents/blob/a44ff79da36356acecbeaef122b1b7c4e68d0496/.textlintrc

動作確認をしつつ用意。適用具合は`npx textlint --print-config`。デフォルト設定も確認できます。

### おわりに
これで手元のコマンドレベルですが、textlintで記事を校正できるようになりました。この記事も`--fix`で修正を適用しつつ完成させています。
