# Commit messages guide

[![Say Thanks!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/RomuloOliveira)

這是一份了解 commit 訊息的重要性和如何更好的撰寫它的指導手冊。

它可以幫助你了解什麼是 commit、為什麼撰寫好的訊息很重要、最好的實踐案例以及一些技巧來計劃和 (重新) 撰寫良好的 commit 紀錄。

## 什麼是“commit”？

簡單來說，commit 就是在本地資料庫中撰寫的檔案的 _快照_。與印象中不同的是，[git 不僅儲存不同版本檔案之間的差異，還儲存了所有檔案的完整版本](https://git-scm.com/book/eo/v1/Ekkomenci-Git-Basics#Snapshots,-Not-Differences)。對於兩個 commit 之間沒有被修改的檔案，git 只儲存指向前一個完全相同的檔案的連結。

下面的圖片展示了 git 如何隨著時間儲存資料，其中每個 “Version” 都是一個 commit：

![](https://i.stack.imgur.com/AQ5TG.png)

## 為什麼 commit 資訊很重要？

- 加快和簡化 code review
- 幫助理解一個變更
- 解釋那些無法只透過程式碼來描述的“為什麼”
- 幫助未來的維護人員明白為什麼以及如何產生的變更，從而使問題排查和除錯更容易

為了最好的效果，我們可以使用下一節中描述的一些好的實踐方式和標準。

## 好的實踐方式

這些是從我的經驗、網路文章和其他指導中整理的一些實踐經驗。如果你有更多的經驗（或持不同意見），請隨時提交 Pull Request 來提供幫助。

### 使用祈使句

```
# Good
Use InventoryBackendPool to retrieve inventory backend
用 InventoryBackendPool 取得存貨
```

```
# Bad
Used InventoryBackendPool to retrieve inventory backend
InventoryBackendPool 被用於取得存貨
```

_不過為什麼要使用祈使句呢？_

commit 訊息描述的效果是這個變更實際上**做**了什麼，而不是被做了什麼。

[Chris Beams 的這篇好文](https://chris.beams.io/posts/git-commit/)為我們提供了一些簡單的句子，可以幫助我們用祈使句寫出更好的 commit 訊息：

```
If applied, this commit will <commit message>
如果通過，這個 commit 將會 <commit 訊息>
```

例子：

```
# Good
If applied, this commit will use InventoryBackendPool to retrieve inventory backend
如果通過，這個 commit 將使用 InventoryBackendPool 獲取庫存
```

```
# Bad
If applied, this commit will used InventoryBackendPool to retrieve inventory backend
如果通過，InventoryBackendPool 將會被用在獲取庫取
```

### 第一個字母大寫

```
# Good
Add `use` method to Credit model
```

```
# Bad
add `use` method to Credit model
```

第一個字母大寫的原因是遵守英文句子開頭使用大寫字母的語法規則。

這種做法可能因人而異、因團隊而異、甚至因語言而異。不管是否大寫，重要的是要制定一個標準並遵守它。

### 僅量做到只看到註釋就可以明白而無需查看變更內容

```
# Good
Add `use` method to Credit model
為 Credit 模型增加 `use` 方法

```

```
# Bad
Add `use` method
增加 `use` 方法
```

```
# Good
Increase left padding between textbox and layout frame
在 textbox 和 layout frame 之間增加向左對齊
```

```
# Bad
Adjust css
調整 css
```

它在許多場景中（例如多次 commit、多個變更和重構）非常有用，可以幫助審查者理解提交者的想法。

### 使用訊息本身來解釋“原因”、“目的”、“方式”和其他的細節

```
# Good
Fix method name of InventoryBackend child classes

Classes derived from InventoryBackend were not
respecting the base class interface.

It worked because the cart was calling the backend implementation
incorrectly.
```

```
# Good
Serialize and deserialize credits to json in Cart

Convert the Credit instances to dict for two main reasons:

  - Pickle relies on file path for classes and we do not want to break up
    everything if a refactor is needed
  - Dict and built-in types are pickleable by default
```

```
# Good
Add `use` method to Credit

Change from namedtuple to class because we need to
setup a new attribute (in_use_amount) with a new value
```

訊息的標題和內容之間用空白行隔開。其他空白行被視為訊息內容的一部分。

像“-”、“*”和“\”這樣的符號可以提高可讀性。

### 避免使用沒有上下文的訊息

```
# Bad
Fix this

Fix stuff

It should work now

Change stuff

Adjust css
```

### 限制每行字數

[這裡建議](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)標題最多使用50個字，內容最多使用72個字。

### 保持語言的一致性

對於專案所有者而言：選擇一種語言並使用該語言撰寫所有的 commit 訊息。理想情況下，它應與程式碼註解、預設翻譯地區 (用於本地化專案) 等相匹配。

對於貢獻者而言：使用與既有 commit 紀錄相同的語言撰寫 commit 訊息。

```
# Good
ababab Add `use` method to Credit model
efefef Use InventoryBackendPool to retrieve inventory backend
bebebe Fix method name of InventoryBackend child classes
```

```
# Good (Portuguese example)
ababab Adiciona o método `use` ao model Credit
efefef Usa o InventoryBackendPool para recuperar o backend de estoque
bebebe Corrige nome de método na classe InventoryBackend
```

```
# Bad (mixes English and Portuguese)
ababab Usa o InventoryBackendPool para recuperar o backend de estoque
efefef Add `use` method to Credit model
cdcdcd Agora vai
```

### 範本

下面是參考範本，最初由 [Tim Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html) 撰寫，出現在 [_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project) 中。

```
用 50 個左右或更少的字來描述變更

如有必要，可以提供更詳細的補充說明，並儘可能將其限定在每行 72 個字左右。
在某些情況下，第一行被視為 commit 的標題，其餘的文字被視為內容主體。
因此，將標題從內容分離出來的空白行就顯得非常重要(除非完全省略內容)。
如若不然，在使用命令列，如 “log”，“shortlog” 以及 “rebase” 的時候，將會很容易混淆。

解釋當前 commit 所解決的問題。
請重點描述產生此變更的原因，而非方式（程式碼解釋了一切）。
是否存在副作用以及其他隱含的影響？
請在這裡將其解釋清楚。

接下來請另起一行。

 - 也可以使用列舉的格式 (bullet point)。

 - 通常使用連字號(-)或星號(*)作為要點段落標記，標記與內容之間留一空格，各要點之間留一空白行。但這取決於你們的約定。

如果你使用問題追蹤器，請將對它們的引用放在底部，如下所示:

Resolves: #123
See also: #456, #789
```

## Rebase vs. Merge

這部分是 Atlassian 的優秀教學(TL;DR)——["Merging vs. Rebasing"](https://www.atlassian.com/git/tutorials/merging-vs-rebasing) 的精華。

![](https://wac-cdn.atlassian.com/dam/jcr:01b0b04e-64f3-4659-af21-c4d86bc7cb0b/01.svg?cdnVersion=hq)

### Rebase

**TL;DR:** 將你的分支逐個應用於基本分支，生成新樹。

![](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=hq)

### Merge

**TL;DR:** 建立一個新的 commit，稱為 _merge commit_（合併提交），其具有兩個分支之間的差異。

![](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=hq)

### 為什麼一些人更喜歡 rebase 而非 merge？

我特別喜歡 rebase 而不是 merge。原因有以下幾點：

* 它的歷史紀錄很"乾淨"，沒有無用的合併 commit。
* _所見即所得_，即在程式碼審查中，所有的變更都能在特定的、有標題的 commit 中找到，避免藏在合併 commit 中的修改。
* 通常 merge 是由提交者執行的，並會為每個轉換成 commit 的 merge 寫準確的訊息。
    * 通常我們不會深挖和複查 merge commit，因此儘量避免使用 merge commit，並確保每個變化點都有它們所屬的 commit 。

### 什麼時候 squash

“Squashing” 是將一系列 commit 壓縮成一個的過程。

它在某些情況下很有用，例如：

- 減少那些很少甚至沒有上下文（拼寫錯誤、格式化、遺失內容）的 commit
- 將單獨的變更連結在一起使它們更通俗易懂
- 重寫 _work in progress_ 的 commit

### 什麼時候避免使用 rebase 或 squash

避免在多人共同開發的共用 commit 或共享分支上使用 rebase 和 squash。rebase 和 squash 會改寫歷史紀錄並覆寫當前的 commit，在共享分支 commit（即推送到遠端倉庫或來自其他分支的 commit）上執行這些操作可能會引起混亂，由於分支產生分岐及衝突，合作者可能會因此失去它們（本地和遠端）的更改。

## 有用的 git 指令

### rebase -i

使用它來壓縮提交（squash commits）、撰寫訊息、重寫/刪除/重新編排 commit 等。

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

使用它可以輕鬆清理 commit，而不需要複雜的 rebase。[這篇文章](http://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html)提供了很好的範例，說明了如何以及何時進行此操作。

### cherry-pick

它在你 commit 到了錯誤的分支而不需要重新撰寫程式碼時非常有用。

例子：

```
$ git cherry-pick 790ab21
[master 094d820] Fix English grammar in Contributing
 Date: Sun Feb 25 23:14:23 2018 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### add/checkout/reset [--patch | -p]

假設我們有以下衝突：

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

我們可以使用 `git add -p` 只加入我們想要的更新，而無需更改已有的程式碼。
它在將一個大的變更分解為小的 commit 或 reset/checkout 特定的變更時很有用。

```
Stage this hunk [y,n,q,a,d,/,j,J,g,s,e,?]? s
Split into 2 hunks.
```

#### hunk 1

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

#### hunk 2

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

#### hunk 3

```diff
@@ -202,3 +205,4 @@ Any kind of help would be appreciated. Example of topics that you can help me wi

 - [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
 - [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
+- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
```

## 其他有趣的內容

https://whatthecommit.com/

## 喜歡它嗎？

[說點感謝！](https://saythanks.io/to/RomuloOliveira)

## 貢獻

感謝任何形式的幫助。例如：

- 語法和拼寫的糾正
- 翻譯成其他語言
- 原引用的改進
- 不正確或不完整的訊息

## 靈感、來源以及補充閱讀

- [如何寫 Git Commit Message](https://chris.beams.io/posts/git-commit/)
- [Pro Git Book - Commit 指導手冊](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
- [關於 Git Commit Messages 的說明](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [merging 與 rebase](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Pro Git Book - 修改歷史紀錄](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
