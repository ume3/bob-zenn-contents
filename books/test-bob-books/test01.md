---
title: "まずはZenn CLIを実行する"
---

# はじめに
[Zenn CLIで記事を書いた](https://zenn.dev/b0b/articles/zenn_cli_test_20230504)ので、今度は本を書きたいとなりました。そのやり方をまとめてみた記事となります。

:::message
Web上ではなく、GitHubリポジトリ連携で本を作成する場合を想定しています。
:::

## 参考記事
- [Zenn CLIで記事・本を管理する方法](https://zenn.dev/zenn/articles/zenn-cli-guide#cli-%E3%81%A7%E6%9C%AC%EF%BC%88book%EF%BC%89%E3%82%92%E7%AE%A1%E7%90%86%E3%81%99%E3%82%8B)
- [Zennで本を執筆する！Webからの本作成マニュアル](https://zenn.dev/zenn/books/how-to-create-book)

## Zenn CLIで本に必要な設定の用意
記事を書いたときと同様にコマンドが用意されています。

```
❯ npx zenn new:book --slug test-bob-books
created: books/test-bob-books/config.yaml
created: books/test-bob-books/example1.md
created: books/test-bob-books/example2.md
```

参考記事より、config.yamlが`new:articles`の時と同様で管理に必要な設定となります。

```bash:cat congig.yaml
❯ cat books/test-bob-books/config.yaml
title: ""
summary: ""
topics: []
published: false
price: 0 # 有料の場合200〜5000
# 本に含めるチャプターを順番に並べましょう
chapters:
  - example1
  - example2
```

あとはそれぞれに必要な項目を記載すれば完成します。

![](/images/books/test-bob-books/start_books01.jpg)

一ページ目はこのような書き出しがpreviewされるようになりました。メタですが、この記事自体がbooksの一ページ目になります。