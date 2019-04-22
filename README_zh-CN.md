# Commit messages guide

[![Say Thanks!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/RomuloOliveira)

一个了解 commit 信息重要性和如何更好地编写它的指南。

它可以帮助你了解什么是 commit、为什么编写好的信息很重要、最好的实践案例以及一些技巧来计划和（重新）编写良好的 commit 历史。

## 可用语言

- [English](README.md)
- [Português](README_pt-BR.md)
- [Deutsch](README_de-DE.md)
- [简体中文](README_zh-CN.md)

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
Use InventoryBackendPool to retrieve inventory backend （用 InventoryBackendPool 获取库存）
```

```
# Bad
Used InventoryBackendPool to retrieve inventory backend （InventoryBackendPool 被用于获取库存）
```

_不过为什么要使用祈使句呢？_

commit 信息描述的是引用的变更部分实际上**做**了什么，它的效果，而不是因此被做了什么。

[Chris Beams 的这篇优秀的文章](https://chris.beams.io/posts/git-commit/)为我们提供了一些简单的句子，可以帮助我们用祈使句编写更好的 commit 信息：

```
If applied, this commit will <commit message> （如获许可，此提交将会 <提交备注>）
```

例子：

```
# Good
If applied, this commit will use InventoryBackendPool to retrieve inventory backend （如获许可，此提交将使用 InventoryBackendPool 获取库存）
```

```
# Bad
If applied, this commit will used InventoryBackendPool to retrieve inventory backend （如获许可，InventoryBackendPool 将会被用于获取库存）
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
Add `use` method to Credit model （为 Credit 模块添加 `use` 方法）

```

```
# Bad
Add `use` method （添加 `use` 方法）
```

```
# Good
Increase left padding between textbox and layout frame （在 textbox 和 layout frame 之间添加向左对齐）
```

```
# Bad
Adjust css （就改了下 css）
```

它在许多场景中（例如多次 commit、多个更改和重构）非常有用，可以帮助审查人员理解提交者的想法。

### 使用信息本身来解释“为什么”、“如何”和其他的细节

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

像“-”、“*”和“\”的字符可以提高可读性。

### 避免使用通用的信息或没有上下文的信息

```
# Bad
Fix this

Fix stuff

It should work now

Change stuff

Adjust css
```

### 限制列数

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

这是一个模板，最初由 [Tim Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html) 编写，出现在 [_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project) 中。

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

## Rebase vs. Merge

这部分是 Atlassian 的优秀教程——["Merging vs. Rebasing"](https://www.atlassian.com/git/tutorials/merging-vs-rebasing) 的精华。

![](https://wac-cdn.atlassian.com/dam/jcr:01b0b04e-64f3-4659-af21-c4d86bc7cb0b/01.svg?cdnVersion=hq)

### Rebase

**精华：** 将你的分支一个接一个地应用于基本分支上，生成一棵新树。

![](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=hq)

### Merge

**精华：** 创建一个新的 commit，称为一个 _merge commit_（合并提交），其中包含了两个分支的差异。

![](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=hq)

### 为什么一些人更喜欢 rebase 而不是 merge？

我特别喜欢 rebase 而不是 merge。原因有以下几点：

* 它会产生一个“干净”的历史记录，没有不必要的合并的 commit。
* _所见即所得_，即在代码审查中，所有的更改都来自于一个特定的、有标题的 commit，避免了在合并 commit 中隐藏的修改。
* 提交者将解决更多的合并，而且每个合并的更改都在 commit 中，并带有适当的信息。
    * 深入观察并审查合并的 commit 很不常见，因此避免它们可以确保所有更改都有一个属于它们的 commit。

### 什么时候 squash

“Squashing” 是将一系列提交压缩成一个提交的过程，

它在很多情况下都很有用，例如：

- 减少那些很少或没有上下文（拼写错误、格式化、缺失内容）的 commit
- 将单独的更改连接在一起使它们更有意义
- 重写 _还在开发_ 的 commit 

### 什么时候避免 rebase 或 squash？

在多人开发的公共 commit 或共享分支上避免 rebase 和 squash。rebase 和 squash 会重写历史和现有的 commit，在共享分支的 commit（即推送到远程仓库或来自其他分支的 commit）可能会导致混乱，而且由于有分支的树和冲突人们可能会失去他们（本地和远程）的更改。

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

假设我们有以下差异：

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

我们可以使用 `git add -p` 只添加我们想要的补丁，而不需要更改已经编写的代码。
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

[Say thanks!](https://saythanks.io/to/RomuloOliveira)

## 贡献

感谢任何形式的帮助。一些你能帮助我的例子：

- 语法和拼写的纠正
- 翻译成其他语言
- 原引用的改进
- 不正确或不完整的信息

## 灵感、来源以及扩展阅读

- [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
- [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Pro Git Book - Rewriting History](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
