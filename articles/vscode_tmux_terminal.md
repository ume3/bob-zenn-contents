---
title: "VSCodeのターミナルでtmuxを使いたい"
emoji: "✋"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["tmux","vscode"]
published: true
published_at: 2023-05-09 10:00 # 未来の日時を指定する
---

# はじめに
普段使うターミナルは[Alacritty](https://github.com/alacritty/alacritty)です。今までiterm+tmuxを使っていたので、その名残でtmuxも使っています。このとき、VSCodeのターミナルを使う際にbashやzshとなるところですが、この経緯もあってtmuxが使いたくなりました。

## 参考記事
- [VScodeの設定（settings\.json）まとめ【2023年4月更新】](https://zenn.dev/sayuki_coding/articles/c389d9ad48feaa)
- [TmuxをVSCodeのTerminalでデフォルトで起動するようにする](https://zenn.dev/suba/articles/ffc5454964787a)

### 設定方法
参考記事より、settings.jsonに設定を加えればいいので以下でOKでした。

```
    "terminal.integrated.defaultProfile.osx": "tmux",
```

![](/images/articles/tmux_on.jpg)

使用環境がMacなので`osx`ですが、Linuxの人は別の設定が用意されています。
この状態でターミナルの設定をした結果、以下の表示反映を確認しました。

![](/images/articles/tmux_add.jpg)

これで、VSCode操作時のターミナルがtmuxになりました。

### おわりに
あとは、エディタとターミナルを行き来するショートカットを用意してVSCode内でターミナル操作も完結するようにしました。今まで塾してきたターミナル設定を再利用できて便利です。画面分割もtmuxで用意したショートカットが反映されていることも確認しました。この機会にtmux卒業も考えましたが、便利に感じているうちはこの設定でターミナル操作を続ける予定です。