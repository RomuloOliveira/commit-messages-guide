# コミットメッセージガイド

[![ありがとう!を言う!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/RomuloOliveira)

コミットメッセージの重要性と良いコミットメッセージの書き方を理解するためのガイドです
(訳注: 本日本語訳では、英語でコミットメッセージを書くことを想定します)

コミットとは何か、良いコミットメッセージを書くことが重要であるのはなぜか、良いコミット履歴を計画し書く(書き直す)ための最良の方法とコツを学ぶのを手助けできるかもしれません。

## 「コミット」とは何か?

簡単に言うと、コミットとはあなたのローカルリポジトリーに書かれたローカルファイルの _スナップショット_ です。
人々が考えているのとは異なり、[gitはファイルの差分のみを保持しているのではなく全てのファイルの全てのバージョンのファイルそのものを保持しています](https://git-scm.com/book/eo/v1/Ekkomenci-Git-Basics#Snapshots,-Not-Differences)。
1つのコミットで以前と変更がないファイルについては、gitは既に保持している以前のバージョンの同一ファイルへのリンクを保持します。

下図は、gitが経時的にデータをどのように保持しているかを示しています。個々の「version」をコミットだと考えてください。

![](https://i.stack.imgur.com/AQ5TG.png)

## なぜコミットメッセージは重要なのか?

- 素早く効率的にコードレビューをするため
- 変更を理解するのを助けるため
- コードのみでは説明できない「なぜ」を説明するため
- 未来のメンテナーが、なぜどのように変更がされたのかを理解し、トラブル解決とデバッグを容易にできるようにするため

これらの成果を最大化するために、次のセクションで説明する良い事例と標準を使うことができます。

## 良い事例

私の経験やインターネット上の記事、他のガイドから集めた良い事例があります。
他に良い事例を知っていたり、賛成できないものがある場合には、気軽にプルリクエストを送って貢献してください。

### 命令形を使う

```
# 良い例
Use InventoryBackendPool to retrieve inventory backend
```

```
# 悪い例
Used InventoryBackendPool to retrieve inventory backend
```

_しかし、なぜ命令法を使うべきなのでしょうか?_

コミットメッセージは、関連付けられる変更が実際に何を*する*のか、どんな効果を持つのかを説明するものであり、何がされたのかを説明するものではありません。

[Chris Beamsによるこの優れた記事](https://chris.beams.io/posts/git-commit/)では、命令形でより良いコミットメッセージを書くのに助けとなるシンプルな例文が示されています。

```
If applied, this commit will <コミットメッセージ>
```

例:

```
# 良い例
If applied, this commit will use InventoryBackendPool to retrieve inventory backend
```

```
# 悪い例
If applied, this commit will used InventoryBackendPool to retrieve inventory backend
```

### 最初の文字を大文字にする

```
# 良い例
Add `use` method to Credit model
```

```
# 悪い例
add `use` method to Credit model
```

最初の文字を大文字にするのは、文の初めの文字は大文字にするという文法規則に従っています。

これは人によりチームにより言語により異なります。
大文字にするにしてもしないにしても、重要なのは1つの標準にこだわり従うことです。

### ソースコードを見ることなく変更を伝えられるようにする

```
# 良い例
Add `use` method to Credit model

```

```
# 悪い例
Add `use` method
```

```
# 悪い例
Increase left padding between textbox and layout frame
```

```
# 悪い例
Adjust css
```

このことは、多くのシナリオ(例えば、複数のコミットやいくつかの変更、リファクタリング)で、コミッターが考えていたことをレビュアーが理解するのを助けます。

### 「なぜ」「何のために」「どのように」その他の詳細を説明するためにメッセージの本文を使う。

```
# 良い例
Fix method name of InventoryBackend child classes

Classes derived from InventoryBackend were not
respecting the base class interface.

It worked because the cart was calling the backend implementation
incorrectly.
```

```
# 良い例
Serialize and deserialize credits to json in Cart

Convert the Credit instances to dict for two main reasons:

  - Pickle relies on file path for classes and we do not want to break up
    everything if a refactor is needed
  - Dict and built-in types are pickleable by default
```

```
# 良い例
Add `use` method to Credit

Change from namedtuple to class because we need to
setup a new attribute (in_use_amount) with a new value
```

メッセージの件名と本文は空行で区切ります。それ以上の空行はメッセージの本文の一部とみなされます。

`-`や`*`、\`といった文字は読みやすくするために使えます。

### 一般的なメッセージや文脈の分からないメッセージを避ける

```
# 悪い例
Fix this

Fix stuff

It should work now

Change stuff

Adjust css
```

### 文字数を制限する

件名は50文字、本文は1行につき72文字を上限とするのが[推奨されています](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)。

### 言語の一貫性を保つ

プロジェクトのオーナーへ: 言語を1つ選び、全てのコミットメッセージにその言語を使ってください。
その言語がコード中のコメントやデフォルトの翻訳ロケール(ローカライズされたプロジェクトの場合)などとも一致している方が良いです。

貢献者へ: 既に存在するコミット履歴の言語を使ってあなたのコミットメッセージを書いてください。

```
# 良い例
ababab Add `use` method to Credit model
efefef Use InventoryBackendPool to retrieve inventory backend
bebebe Fix method name of InventoryBackend child classes
```

```
# 良い例 (ポルトガル語の例)
ababab Adiciona o método `use` ao model Credit
efefef Usa o InventoryBackendPool para recuperar o backend de estoque
bebebe Corrige nome de método na classe InventoryBackend
```

```
# 悪い例 (英語とポルトガル語が混在している)
ababab Usa o InventoryBackendPool para recuperar o backend de estoque
efefef Add `use` method to Credit model
cdcdcd Agora vai
```

### テンプレート

これは[元々Tim Popeによって書かれた](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)テンプレートで、[_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project)に収録されています。

```
Summarize changes in around 50 characters or less

More detailed explanatory text, if necessary. Wrap it to about 72
characters or so. In some contexts, the first line is treated as the
subject of the commit and the rest of the text as the body. The
blank line separating the summary from the body is critical (unless
you omit the body entirely); various tools like `log`, `shortlog`
and `rebase` can get confused if you run the two together.

Explain the problem that this commit is solving. Focus on why you
are making this change as opposed to how (the code explains that).
Are there side effects or other unintuitive consequences of this
change? Here's the place to explain them.

Further paragraphs come after blank lines.

 - Bullet points are okay, too

 - Typically a hyphen or asterisk is used for the bullet, preceded
   by a single space, with blank lines in between, but conventions
   vary here

If you use an issue tracker, put references to them at the bottom,
like this:

Resolves: #123
See also: #456, #789
```

## リベース対マージ

このセクションは、Atlassianの優れたチュートリアルである["Merging vs. Rebasing"](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)をまとめたものです。

![](https://wac-cdn.atlassian.com/dam/jcr:01b0b04e-64f3-4659-af21-c4d86bc7cb0b/01.svg?cdnVersion=hq)

### リベース

**まとめ**: あなたのブランチのコミットを1つ1つベースのブランチに追加して、新しいツリーを生成します。

![](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=hq)

### マージ

**まとめ**: 適切には _マージコミット_ と呼ばれる、2つのブランチの間の差分である新しいコミットを作成します。

![](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=hq)

### なぜマージよりリベースを好む人々がいるのか?

私は特にマージよりリベースの方が良いと考えています。理由は以下の通りです。

* リベースは「クリーン」な履歴を生成し、不必要なマージコミットを生成しない
* 見たままが得られる、つまり、コードレビューで全ての変更が特定のコミットと関連付けられ、マージコミットに変更が隠れるのを防げる
* コミッターによりマージがされるにつれて、それぞれのマージの変更は適切なメッセージを持った1つのコミットにまとまってしまう
    * マージコミットを掘り起こしたり、レビューしたりすることは通常やるべきことではない。それを避けるために、全ての変更はそれぞれのコミットを持つようにする

### スカッシュすべき時

「スカッシュ」とは、一連のコミットを1つのコミットまとめるプロセスです。

これは、以下の例のような状況では一般的です。

- 文脈が乏しいまたはないコミットをなくす (誤字を訂正する、フォーマットを整える、忘れていたものを含める)
- 一緒に適用された方がより意味が明確になる分かれた変更をまとめる
- _作業中_ のコミットを書き直す

### リベースやスカッシュを避けるべき時は?

リベースやスカッシュは、公開されたコミットまたは複数の人が作業している共有されたブランチでは避けてください。
リベースやスカッシュは履歴を書き換え、既存のコミットを上書きします。
これを共有されたブランチで行うと混乱をまねき(つまり、コミットはリモートリポジトリーにプッシュされるし、リモートリポジトリーは他の人のブランチから生成される)、ツリーの状態が一貫性を失い競合が発生することで、他の人が自分の変更を(ローカルとリモートの両方で)失うかもしれません。

## 有用なgitコマンド

### rebase -i

コミットをスカッシュしたり、メッセージを編集したり、コミットを書き換えたり、削除したり、並べ替えたりするために使います。

```
pick 002a7cc Improve description and update document title
pick 897f66d Add contributing section
pick e9549cf Add a section of Available languages
pick ec003aa Add "What is a commit" section"
pick bbe5361 Add source referencing as a point of help wanted
pick b71115e Add a section explaining the importance of commit messages
pick 669bf2b Add "Good practices" section
pick d8340d7 Add capitalization of first letter practice
pick 925f42b Add a practice to encourage good descriptions
pick be05171 Add a section showing good uses of message body
pick d115bb8 Add generic messages and column limit sections
pick 1693840 Add a section about language consistency
pick 80c5f47 Add commit message template
pick 8827962 Fix triple "m" typo
pick 9b81c72 Add "Rebase vs Merge" section

# Rebase 9e6dc75..9b81c72 onto 9e6dc75 (15 commands)
#
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into the previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
# d, drop = remove commit
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```

#### fixup

もっと複雑なリベースを必要とせず、簡単にコミットを綺麗にするために使います。
[この記事](http://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html)はどのように、どういう時に使うべきかのとても良い例を示しています。

### cherry-pick

間違って別のブランチでしてしまったコミットをコードを書き直すことなく適用させるのにとても便利です。

例:

```
$ git cherry-pick 790ab21
[master 094d820] Fix English grammar in Contributing
 Date: Sun Feb 25 23:14:23 2018 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### add/checkout/reset [--patch | -p]

以下のような差分があるとします。

```diff
diff --git a/README.md b/README.md
index 7b45277..6b1993c 100644
--- a/README.md
+++ b/README.md
@@ -186,10 +186,13 @@ bebebe Corrige nome de método na classe InventoryBackend
 ``
 # Bad (mixes English and Portuguese)
 ababab Usa o InventoryBackendPool para recuperar o backend de estoque
-efefef Add `use` method to Credit model
 cdcdcd Agora vai
 ``

+### Template
+
+This is a template, [written originally by Tim Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), which appears in the [_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project).
+
 ## Contributing

 Any kind of help would be appreciated. Example of topics that you can help me with:
@@ -202,3 +205,4 @@ Any kind of help would be appreciated. Example of topics that you can help me wi

 - [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
 - [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
+- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
```

`git add -p`を使うことで、必要なパッチのみ追加することができ、既に書かれたコードを変更する必要はありません。
これは大きな変更をより小さなコミットに分割するのに役立ちますし、特定の変更をreset/checkoutするのにも役立ちます。

```
Stage this hunk [y,n,q,a,d,/,j,J,g,s,e,?]? s
Split into 2 hunks.
```

#### 部分1

```diff
@@ -186,7 +186,6 @@
 ``
 # Bad (mixes English and Portuguese)
 ababab Usa o InventoryBackendPool para recuperar o backend de estoque
-efefef Add `use` method to Credit model
 cdcdcd Agora vai
 ``

Stage this hunk [y,n,q,a,d,/,j,J,g,e,?]?
```

#### 部分2

```diff
@@ -190,6 +189,10 @@
 ``
 cdcdcd Agora vai
 ``

+### Template
+
+This is a template, [written originally by Tim Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), which appears in the [_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project).
+
 ## Contributing

 Any kind of help would be appreciated. Example of topics that you can help me with:
Stage this hunk [y,n,q,a,d,/,K,j,J,g,e,?]?

```

#### 部分3

```diff
@@ -202,3 +205,4 @@ Any kind of help would be appreciated. Example of topics that you can help me wi

 - [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
 - [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
+- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
```

## その他の有用なこと

https://whatthecommit.com/

## 気に入りましたか?

[ありがとう!を言う](https://saythanks.io/to/RomuloOliveira)

## 貢献する

どんな種類の手助けも歓迎します。例えば以下の事項で手助けしてください。

- 文法と綴りの訂正
- 他の言語への翻訳
- 他の情報源への参照の改善
- 間違っていたり不完全であったりする情報の訂正

## インスピレーションや情報源、次に読むべきもの

- [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
- [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Pro Git Book - Rewriting History](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
