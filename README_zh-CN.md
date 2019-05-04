# Commit messages guide

[![Say Thanks!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/RomuloOliveira)

一个了解 commit 信息重要性和如何更好地编写它的指南。

它可以帮助你了解什么是 commit、为什么编写好的信息很重要、最好的实践案例以及一些技巧来计划和（重新）编写良好的 commit 历史。

## 什么是“commit”？

简单来讲，commit 就是在本地存储库中编写的文件的 _快照_。与印象中不同的是，[git 不仅存储不同版本文件之间的差异，还存储了所有文件的完整版本](https://git-scm.com/book/eo/v1/Ekkomenci-Git-Basics#Snapshots,-Not-Differences)。对于两个 commit 之间没有被修改的文件，git 只存储指向前一个完全相同的文件的链接。

下面的图片展示了 git 如何随着时间存储数据，其中每个 “Version” 都是一个 commit：

![](https://i.stack.imgur.com/AQ5TG.png)

## 为什么 commit 信息很重要？

- 加快和简化代码审查（code reviews）
- 帮助理解一个更改
- 解释不能只由代码描述的“为什么”
- 帮助未来的维护人员弄清楚为什么以及如何产生的更改，从而使故障排查和调试更容易

为了最大化这些结果，我们可以使用下一节中描述的一些好的实践和标准。

## 好的实践

这些是从我的经验、互联网文章和其他指南中整理的一些实践经验。如果你有更多的经验（或持不同意见），请随时提交 Pull Request 提供帮助。

### 使用祈使句

```
# Good
Use InventoryBackendPool to retrieve inventory backend
用 InventoryBackendPool 获取库存
```

```
# Bad
Used InventoryBackendPool to retrieve inventory backend 
InventoryBackendPool 被用于获取库存
```

_不过为什么要使用祈使句呢？_

commit 信息描述的是引用的变更部分实际上**做**了什么，它的效果，而不是因此被做了什么。

[Chris Beams 的这篇优秀的文章](https://chris.beams.io/posts/git-commit/)为我们提供了一些简单的句子，可以帮助我们用祈使句编写更好的 commit 信息：

```
If applied, this commit will <commit message> 
如获许可，此提交将会 <提交备注>
```

例子：

```
# Good
If applied, this commit will use InventoryBackendPool to retrieve inventory backend
如获许可，此提交将使用 InventoryBackendPool 获取库存
```

```
# Bad
If applied, this commit will used InventoryBackendPool to retrieve inventory backend 
如获许可，InventoryBackendPool 将会被用于获取库存
```

### 首字母大写

```
# Good
Add `use` method to Credit model
```

```
# Bad
add `use` method to Credit model
```

首字母大写的原因是遵守英文句子开头使用大写字母的语法规则。

这种做法可能因人而异、因团队而异、甚至因语言而异。不管是否大写，重要的是要制定一个标准并遵守它。

### 尽量做到只看注释便可明白而无需查看变更内容

```
# Good
Add `use` method to Credit model 
为 Credit 模块添加 `use` 方法

```

```
# Bad
Add `use` method 
添加 `use` 方法
```

```
# Good
Increase left padding between textbox and layout frame 
在 textbox 和 layout frame 之间添加向左对齐
```

```
# Bad
Adjust css 
就改了下 css
```

它在许多场景中（例如多次 commit、多个更改和重构）非常有用，可以帮助审查人员理解提交者的想法。

### 使用信息本身来解释“原因”、“目的”、“手段”和其他的细节

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

信息的主题和正文之间用空行隔开。其他空行被视为信息正文的一部分。

像“-”、“*”和“\”这样的字符可以提高可读性。

### 避免使用无上下文的信息

```
# Bad
Fix this

Fix stuff

It should work now

Change stuff

Adjust css
```

### 限制每行字数

[这里建议](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)主题最多使用50个字符，正文最多使用72个字符。

### 保持语言的一致性

对于项目所有者而言：选择一种语言并使用该语言编写所有的 commit 信息。理想情况下，它应与代码注释、默认翻译区域（用于本地化项目）等相匹配。

对于贡献者而言：使用与现有 commit 历史相同的语言编写 commit 信息。

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

### 模板

下面是参考模板，最初由 [Tim Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html) 编写，出现在 [_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project) 中。

```
用 50 左右或更少的字符描述更改

如有必要，可提供更详细的补充说明，并尽可能将其限定在每行 72 个字符左右。
在某些情况下，第一行被视为 commit 的主题，文本其余部分被作为正文。
因此，将主题从正文分割出来的空白行就显得至关重要(除非完全省略正文)。
如若不然，在使用命令行，如 “log”，“shortlog” 以及 “rebase” 的时候，将会很容易混淆。

解释当前 commit 所解决的问题。
请重点描述产生此更改的原因，而非手段（代码解释了一切）。
是否存在副作用以及其他不直观的影响？
请在这里将其解释清楚。

接下来请另起一行。

 - 也可以使用列举要点的格式。

 - 通常使用连字符(-)或星号(*)作为要点段落标记，标记与文本之间留一空格，各要点之间留一空行。但这取决于你们的约定。

如果你使用问题跟踪器，请将对它们的引用放在底部，如下所示:

Resolves: #123
See also: #456, #789
```

## Rebase vs. Merge

这部分是 Atlassian 的优秀教程(TL;DR)——["Merging vs. Rebasing"](https://www.atlassian.com/git/tutorials/merging-vs-rebasing) 的精华。

![](https://wac-cdn.atlassian.com/dam/jcr:01b0b04e-64f3-4659-af21-c4d86bc7cb0b/01.svg?cdnVersion=hq)

### Rebase

**TL;DR:** 将你的分支逐个应用于基本分支，生成新树。

![](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=hq)

### Merge

**TL;DR:** 创建一个新的 commit，称为 _merge commit_（合并提交），其具有两个分支之间的差异。

![](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=hq)

### 为什么一些人更喜欢 rebase 而非 merge？

我特别喜欢 rebase 而不是 merge。原因有以下几点：

* 它的历史信息很"干净"，没有无用的合并 commit。
* _所见即所得_，即在代码审查中，所有的更改都能在特定的、有标题的 commit 中找到，避免了隐藏在合并 commit 中的修改。
* 通常 merge 是由提交者实行的，并会为每个转换成 commit 的 merge 书写准确的信息。
    * 通常我们不会深挖和复查 merge commit，因此尽量避免使用 merge commit，并确保个变化点都有它们所属的 commit 。

### 什么时候 squash

“Squashing” 是将一系列 commit 压缩成一个的过程。

它在某些情况下很有用，例如：

- 减少那些很少甚至没有上下文（拼写错误、格式化、缺失内容）的 commit
- 将单独的更改连接在一起使它们更通俗易懂
- 重写 _work in progress_ 的 commit 

### 什么时候避免 rebase 或 squash

避免在多人共同开发的公共 commit 或共享分支上使用 rebase 和 squash。rebase 和 squash 会改写历史记录并覆盖当前 commit，在共享分支的 commit（即推送到远程仓库或来自其他分支的 commit）上执行这些操作可能会引起混乱，由于分支产生分歧及冲突，合作者可能会因此失去他们（本地和远程）的更改。

## 有用的 git 命令

### rebase -i

使用它来压缩提交（squash commits）、 编写信息、 重写/删除/重新编排 commit 等。

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

使用它可以轻松清理 commit，而不需要复杂的 rebase。[这篇文章](http://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html)提供了很好的示例，说明了如何以及何时进行此操作。

### cherry-pick

它在你 commit 到了错误的分支而不需要重新编码时非常有用。

例子：

```
$ git cherry-pick 790ab21
[master 094d820] Fix English grammar in Contributing
 Date: Sun Feb 25 23:14:23 2018 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### add/checkout/reset [--patch | -p]

假设我们有以下冲突：

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

我们可以使用 `git add -p` 只添加我们想要的补丁，而无需更改已有代码。
它在将一个大的更改分解为小的 commit 或 reset/checkout 特定的更改时很有用。

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

## 其他有趣的内容

https://whatthecommit.com/

## 喜欢它吗？

[点赞！](https://saythanks.io/to/RomuloOliveira)

## 贡献

感谢任何形式的帮助。例如：

- 语法和拼写的纠正
- 翻译成其他语言
- 原引用的改进
- 不正确或不完整的信息

## 灵感、来源以及扩展阅读

- [如何编写 Git Commit Message](https://chris.beams.io/posts/git-commit/)
- [Pro Git Book - Commit 指南](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
- [关于 Git Commit Messages 的说明](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [合并与变基](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Pro Git Book - 改写历史](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
