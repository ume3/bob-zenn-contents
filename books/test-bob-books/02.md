---
title: "カバー画像を導入する"
---

## カバー画像を用意する
[参考記事](https://zenn.dev/zenn/articles/zenn-cli-guide#%F0%9F%96%BC%EF%B8%8F-%E3%82%AB%E3%83%90%E3%83%BC%E7%94%BB%E5%83%8F)より、booksのカバー画像も用意してみます。推奨サイズおよびjpg, png指定がある点は注意です。
なお、参考記事のbooksの[ディレクトリ配置が参考](https://github.com/zenn-dev/zenn-docs/blob/main/books/how-to-create-book/cover.jpg)になります。これだけが特殊なファイル名になります。

![](/images/books/test-bob-books/start_books02.jpg)

VSCode+Zennの連携をしていれば、カバー画像がないことを警告してくれますので、気がつくことができます。
ここでもメタですが、この本を作って公開する際にはカバー画像が表示されていることでしょう。

なお、配置箇所は以下となりました。

```bash:tree
❯ tree books/test-bob-books/
books/test-bob-books/
├── 01.md
├── 02.md
├── config.yaml
└── cover.jpg
```

この`cover.jpg`の引用元はこちらになります（著作権保護期間は満了）。

> https://www.dl.ndl.go.jp/api/iiif/1899550/R0000014/1976,510,1496,2312/,766/0/default.jpg
> 葛飾北齋 画『北斎模様画譜』,探古堂,1884.8. 国立国会図書館デジタルコレクション https://dl.ndl.go.jp/pid/1899550 (参照 2023-05-06)

# おわりに
本を作ることそのものを記事にしてまとめてみました。このように、Zennでは手軽に本も作成できます。今回は公開設定ですが、非公開設定＋プライス設定も可能なようです。GitHubで執筆する際は、public設定ではなくprivate設定で管理するのが定石のようです。
