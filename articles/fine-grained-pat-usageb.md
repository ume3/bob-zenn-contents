---
title: "GitHubにgit pushするためだけのFine-grained PATsの権限設定のやり方"
emoji: "⛳"
type: "tech"
topics: ["github","git","token"]
published: true
published_at: 2023-05-06 10:00
---

## はじめに
GitHubにCLIから`git push`するときのつまずきはいくつかあると思います。
定番は以下のような403エラーです。

```
❯ git push -u origin main
remote: Permission to ume3/bob-zenn-contents.git denied to ume3.
fatal: unable to access 'https://github.com/ume3/bob-zenn-contents.git/': The requested URL returned error: 403
```

よくある対応はGitHub名+パスワードによる認証。ではなく、[アクセストークンを用います](https://docs.github.com/ja/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token#creating-a-fine-grained-personal-access-token)。これは、[2021年8月から認証方式の変化](https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/)の影響です。
さらに[2022年10月](https://github.blog/2022-10-18-introducing-fine-grained-personal-access-tokens-for-github/)には、新しい`Personal access tokens (PATs)`が登場しました。

久しぶりにリポジトリをこしらえて`git pull`するとこの変化を目の当たりにしたのでまとめてみます。

### 新しいPATsとは
fine-grained personal access tokens in Public Betaのことです。

[personal access tokenの種類](https://docs.github.com/ja/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token#personal-access-token-%E3%81%AE%E7%A8%AE%E9%A1%9E)より以下、引用します。

> 現在、GitHub では、2 種類のpersonal access token (fine-grained personal access token と personal access tokens (classic)) がサポートされています。 GitHub では、可能な限り、personal access tokens (classic) ではなく fine-grained personal access token を使用することをお勧めします。
> 引用：https://docs.github.com/ja/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token#personal-access-token-%E3%81%AE%E7%A8%AE%E9%A1%9E

![](/images/articles/pats_new_main.jpg)

- personal access tokens (classic)  ... 今まで使っていたtoken
- fine-grained personal access token ... これが新しいtoken。なお、2023年5月確認時はβ版。

このアクセストークンは適切な権限設定が必要です。
classicであれば、そのやりかたが染み付いていたのですが、今回は新しいやり方で設定することにしました。

### 参考記事
- [Introducing fine\-grained personal access tokens for GitHub \| The GitHub Blog](https://github.blog/2022-10-18-introducing-fine-grained-personal-access-tokens-for-github/)

#### New fine-grained personal access token (Beta)
やりたいことはbranchを`git push`でファイルをアップロードしたいだけです。そのための権限は最小にしたいです。

まずはGitHub上で、[New fine-grained personal access token](https://github.com/settings/personal-access-tokens/new)を選択。
マニュアルと参考記事より、`Repository access`は、`Only select repositories`を選択。`Permissions`をカスタマイズします。

#### 最小設定： Repository permissionsに Read and Write access to codeするだけ
`Account permissions`は設定不要です。`Repository permissions`を選択。設定する箇所は一箇所だけです。

![](/images/articles/contens_only.jpg)

`Contents(Repository contents, commits, branches, downloads, releases, and merges.)`の設定を`Read and Write`にすればOK。

![](/images/articles/repo_permissions_simple.jpg)

この設定になっていればOKです。なお、`Read access to metadata`は必須設定で自動付与されます。
あとは発行されたtokenをコピーして、git pullの際に利用（設定方法はいろいろありますが今回は省略）すればOKです。

#### workflowsにも設定変更を適用したいとき
なお、このtokenの権限だと`.github/workflows`を編集する権限がありません。

```
 ! [remote rejected] add-reviewdog -> add-reviewdog (refusing to allow a Personal Access Token to create or update workflow `.github/workflows/reviewdog.yml` without `workflow` scope)
error: failed to push some refs to 'https://github.com/ume3/bob-zenn-contents.git'
```

このようなエラーが出て、`git pull`でworkflowsのymlを保存できませんでした。
以下の権限設定が最下部にありましたので付与すると動きます。

- Workflows (Update GitHub Action workflow files.)

こちらも、`Access: Read and Write`の権限を付与することで`git pull`できるようになりました。最終的な設定は以下となります。

![](/images/articles/overview_last.jpg)

### おわりに
personal access tokens (classic) でしか権限を設定したことがないので、いざ新しいやり方をしたときにつまずきました。意外とネットで検索しても出てこなかったので今回まとめております。誰かの役に立てばうれしいです。


