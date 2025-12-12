---
title: "生成AIツールの利用規約の読み方の進め方"
emoji: "📋"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["ai", "privacy"]
published: true
---

## はじめに

この記事は [GENDA Advent Calendar 2025 シリーズ1 Day 13](https://qiita.com/advent-calendar/2025/genda) の記事です。

株式会社GENDA EMのボブです。2025年はたくさんの生成AIツールが登場しましたね。

生成AIツールの個人プランを利用する際には、ツールによっては入力データがモデルの改善に利用される設定がデフォルトになっていることがあります。そこで、この記事では、個人で生成AIツールを使う際に、入力データの扱いがどこで定義されているのか（利用規約・設定）を確認するための具体的なポイントを紹介します。

## なぜ生成AIに入力したデータの扱いを確認するのか

生成AIツールを使う際に、入力したコードやプロンプトが、モデルの改善や品質向上の目的で利用されるかどうかは気になるところです。

たとえば、開発中のコードや、まだ公開したくないアイデアを含むプロンプトを入力する場合、それらがモデル改善に利用される設計になっているとします。この場合、意図せず情報の性質が抽象化・一般化され、間接的に第三者の出力に影響を与える可能性は完全には否定できません。また、機密情報や個人情報が含まれる可能性がある場合、データの取り扱い次第では、想定外のリスクにつながる可能性もあります。

そのため、個人で使う際にも、自分のデータがどう扱われるかを理解したうえでツールを選び、適切に設定したいところです。

## 利用規約やプライバシーポリシーを読む際のポイント

データの扱いを確認するには、利用規約（Terms of Use）とプライバシーポリシー（Privacy Policy）を読むことが重要です。ツールを使う際には、必ずこれらのリンクが提供されています。ツールのインストールやログインのタイミングで、入力したデータがモデル改善に利用されるかどうかを確認することで、ツールを選ぶ際の判断材料を得ることができます。

利用規約やプライバシーポリシーを読む際、調べた限りだと以下の共通用語が登場します。

- **Opt-in(opting)/Opt-out(opt out)**：ユーザーが明示的に同意するか（オプトイン）、デフォルトで有効で拒否できるか（オプトアウト）
- **Model Training**：ユーザーの入力データや会話履歴を、AIモデル自体の性能向上（学習）に利用するかどうか

なお、注意点として、利用規約やプライバシーポリシーは更新されるものです。常にこれらの箇所がどう変わったかを利用継続の際には気にする必要があります。その上で、具体的にツールの設定と規約を見ていきましょう。

### Cursor

[Cursor](https://cursor.com/)では、「Privacy Mode」という言葉でデータ利用に関する設定がまとまっています。

設定確認箇所は以下の通りです。

![Cursorの設定画面](./images/articles/cursor-settings.png)

1. Cursorの設定画面を開く（画面右上の歯車アイコンをクリックするか、`Ctrl + Shift + J`（Windows/Linux）または`Cmd + Shift + J`（Mac）を押す）
2. 設定画面で「General」タブを選択
3. 「Privacy Mode」のオプションを見つけて、選択

CursorのPrivacy Modeでは、コードがモデル学習やプロダクト改善に利用されない設計であることが示されています。一方で、Background Agentなどの機能を提供する目的で、一定期間コードが保存される可能性があることも明記されています。ちなみに、過去にポリシー変更があったこともあり、古いポリシーに沿った設定は、Privacy Mode (Legacy)という名前で区別されています。

利用規約の詳細は、[こちら](https://cursor.com/ja/data-use)で確認できます。なお、「Privacy Mode」の詳細は[Security](https://cursor.com/ja/security)に記載されています。

### Claude

[Claude](https://claude.com/product/overview)では、「Model Training」という言葉でデータ利用に関する情報がまとまっています。

過去に、個人プランでの利用規約変更があり、[2025年9月28日にプライバシーポリシーが更新](https://privacy.claude.com/en/articles/10301952-updates-to-our-privacy-policy)されました。個人向け製品（Claude Free、Pro、Maxなど）では、ユーザーが選択した場合にチャットやコーディングセッションを[Claudeの改善に協力できるようになりました](https://privacy.claude.com/en/articles/10023580-is-my-data-used-for-model-training)。そのため、自分のデータがClaudeの改善に利用してもよいかどうかを選択することが重要です。

Claudeを利用する場合、[マニュアル](https://privacy.claude.com/en/articles/12109829-how-do-i-change-my-model-improvement-privacy-settings)に沿うと、WebUI/Claude Desktop経由だと設定 > プライバシーに「Claudeの改善にご協力ください」という項目があります。この設定を確認することで、自分のデータがClaudeの改善に利用されるかどうかを選択できます。claudeコマンドをインストールする際にも、利用規約を確認することをオススメします。

なお、注意点として、個人向け（Claude Free, Pro & Max plans）と法人向け（API, Console, Team & Enterprise plans）でモデルトレーニングのヘルプの文言が異なります。サポートサイトを検索する際は、個人向けの情報を確認するとよいです。

- [Consumers](https://privacy.claude.com/en/articles/10023580-is-my-data-used-for-model-training)
- [Commercial Customers](https://privacy.claude.com/en/articles/7996868-is-my-data-used-for-model-training)

Claudeのケースのように、途中でポリシーが変わったり、多種多様な製品群より案内文の内容が異なる可能性もあるため、確認時は注意が必要です。

### Google Antigravity

[Antigravity](https://antigravity.google/)では、**「Telemetry」**や**「Interactions data」**という言葉でまとまっています。

インストール時に利用規約とプライバシーポリシーへの同意を求められます。これは、「データ収集・AIモデル改善利用」への明確なオプトイン画面となります。初期状態では「Enable Telemetry」がONでモデル学習に利用されます。しかし、設定画面で「Enable Telemetry」をOFFにすることでオプトアウトが可能な設計です。

利用規約（[Terms of Use](https://antigravity.google/terms)）には以下のように明記されています。

> If you don't want your Interactions used in this way, navigate to settings to change your preference on how such data is used.

![Antigravityの設定画面](./images/articles/antigravity-settings.png)

インストール時の同意と実際の設定画面の両方を確認することが重要です。インストール時に同意したとしても、後から設定画面で変更できることを理解しておく必要があります。

## まとめ
生成AIツールを使い始めるときには、入力データがモデル改善に利用されるかどうかを確認することが、安心して利用するための第一歩となります。

今回は、利用規約やプライバシーポリシーを読む際のポイントを紹介しました。利用規約は変わるため、定期的に確認する必要があります。その際に今回紹介した共通の用語を抑えておくと、それぞれのツールでどういう言葉として表現されているかを読み解く際に役立ちます。設定する際にも迷うことが減ると思います。

この記事が、生成AIツールを安全かつ適切に使い始めるときの参考になれば幸いです。
