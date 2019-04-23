# Commit message guide

[![Say Thanks!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/RomuloOliveira)

这份指南的目的是希望我们了解提交信息的重要性以及如何去编写好它们。

它可以帮助您了解提交的内容，为什么要编写好的消息的重要性，最佳实践，一些技巧和（重新）编写良好的提交历史记录等。

## 可用的语言翻译版本

- [英语](README.md)
- [葡萄牙语](README_pt-BR.md)
- [德语](README_de-DE.md)
- [西班牙语](README_es-AR.md)
- [意大利语](README_it-IT.md)
- [简体中文](README_zh.md)
  
## 什么是“提交”？

简单的说，提交是写在本地存储库中的本地文件的快照。
与某些人的想法相反，[git不仅存储文件之间的差异，同时也存储所有文件的完整版本](https://git-scm.com/book/eo/v1/Ekkomenci-Git-Basics#Snapshots,-Not-Differences)。
对于没有从一个提交更改到另一个提交的文件，git只存储到已经存储的相同文件的链接。

下图显示了git如何随着时间存储数据，其中每个“Version”都是一个提交:

![](https://i.stack.imgur.com/AQ5TG.png)

## 提交时的信息为什么那么重要？

- 加快和简化代码评审
- 帮助了解变化
- 解释无法只用代码描述的“为什么”
- 帮助将来的维护人员找出为什么以及如何进行更改，从而使故障排除和调试更加容易

为了最大化这些结果，我们可以使用下一节中描述的一些好的实践和标准。

## 良好的实践

以下这些是从我的经验、网络文章和其他指南中收集的一些实践。如果您有其他人(或不同意其中一些人)，请随意打开Pull请求并做出贡献。

### 使用必要的形式

```
# Good
Use InventoryBackendPool to retrieve inventory backend
```

```
# Bad
Used InventoryBackendPool to retrieve inventory backend
```

_但是为什么要使用祈使句_

一个提交信息的描述应该是引用的更改实际上**做了什么**，它的影响，而不是已经做了什么。

[Chris Beams的这篇优秀文章](https://chris.beams.io/posts/git-commit/)给我们一个简单的句子，可以用来帮助我们在命令式的环境下写更好的提交信息:

```
If applied, this commit will <commit message> (如果应用了，该提交将 <提交消息>)
```

例如：

```
# Good
If applied, this commit will use InventoryBackendPool to retrieve inventory backend
```

```
# Bad
If applied, this commit will used InventoryBackendPool to retrieve inventory backend
```

### 首字母大写

```
# Good
Add 'use' method to Credit model
```

```
# Bad
add `use` method to Credit model
```

第一个字母应该大写的原因是遵循句子开头使用大写字母的语法规则。

这种做法的使用可能因个人、团队甚至语言的不同而有所不同。无论大写与否，重要的一点是坚持一个标准并遵循它。

### 尝试在不查看源代码的情况下跟别人交流更改的功能

```
# Good
Add `use` method to Credit model (将`use`方法添加到Credit model中)

```

```
# Bad
Add `use` method (添加`use`方法)
```

```
# Good
Increase left padding between textbox and layout frame (增加文本框和布局框架之间的左内边距)
```

```
# Bad
Adjust css (调整css)
```

在许多场景中(例如多个提交、多个更改和重构)，帮助审阅人员理解提交者的想法是非常有用的。

### 使用消息体来解释“为什么”，“为了什么”，“如何”以及更多细节

```
# Good
Fix method name of InventoryBackend child classes 
(修正了InventoryBackend子类的方法名)

Classes derived from InventoryBackend were not
respecting the base class interface.
(从InventoryBackend类派生的子类不尊重基类接口)

It worked because the cart was calling the backend implementation
incorrectly.
(这是cart调用后端实现不正确而导致的)
```

```
# Good
Serialize and deserialize credits to json in Cart 
(在Cart中将credits序列化和反序列化为json)

Convert the Credit instances to dict for two main reasons:
(将Credit实例转换为dict有两个主要原因)

  - Pickle relies on file path for classes and we do not want to break up
    everything if a refactor is needed
    (Pickle依赖于类的文件路径，我们不希望拆分如果需要重构，一切都可以)
  - Dict and built-in types are pickleable by default
    (默认情况下，Dict和内置类型是可选择的)
```

```
# Good
Add `use` method to Credit (在Credit中添加`use`方法)

Change from namedtuple to class because we need to
setup a new attribute (in_use_amount) with a new value
(从namedtuple更改为class，因为我们需要用一个新值设置一个新属性(in_use_amount))
```


消息的主体和主体之间用空行隔开。额外的空行被认为是消息主体的一部分。

像`-`，`*`和`\`这样的字符是提高可读性的元素。

### 避免通用消息或没有上下文的消息

```
# Bad
Fix this

Fix stuff

It should work now

Change stuff

Adjust css
```

### 限制列的数量

[这里推荐](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)主题最多使用50个字符，正文最多使用72个字符。

### 保持语言的一致性

对于项目所有者：选择一种语言并使用该语言编写所有提交消息。理想情况下，它应该匹配代码注释、缺省翻译语言环境(用于本地化的项目)等。

对于贡献者:使用与现有提交历史相同的语言编写提交消息。

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

这是一个模板，[由Tim Pope最初编写](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)，出现在[_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project)书籍中。

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
```
用50个字符或更少的字符总结更改

如有必要，提供更详细的说明文本。将它包装成大约72个字符。
在某些上下文中，第一行作为提交的主题，其余的文本作为主体。
分隔摘要和正文的空白行非常重要(除非完全省略正文);
如果同时运行“log”、“shortlog”和“rebase”等工具，可能会混淆。

解释此提交正在解决的问题。
关注你为什么所做的更改与(代码解释的)方式相反。
是否有副作用或其他不直观的后果更改？ 
这是解释它们的地方。

接下来的段落在空行之后。

 - 要点也可以

 - 通常使用连字符或星号作为项目符号，前面有一个空格，
   中间有空行，但约定在这里有所不同

如果您使用问题跟踪器，请将对它们的引用放在底部，如下所示:

Resolves: #123
See also: #456, #789
```

## 变基与合并

本节是Atlassian的优秀教程[“合并与重基”](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)的**TL;DR**。
(译者注：TL;DR的意思是“文章太长了，读不下去”，所以只显示整篇文章的**精华**或**总结**)

![](https://wac-cdn.atlassian.com/dam/jcr:01b0b04e-64f3-4659-af21-c4d86bc7cb0b/01.svg?cdnVersion=hq)

### 变基（Rebase）

**TL;DR** 将分支提交逐个应用于基本分支，生成新树。

![](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=hq)

### 合并（Merge）

**TL;DR** 创建一个新的提交，称为（适当）合并提交，具有两个分支之间的差异。

![](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=hq)

### 为什么有些人更喜欢变基(Rebase)而不是合并(Merge)？

相较于合并（merge），我更钟情于变基（rebase）的原因包括以下几点：

* 它生成一个“干净”的历史记录，没有不必要的合并提交
* _所看即所得_，在代码评审中，所有更改都来自一个特定的、有标题的提交，避免了合并提交中隐藏的更改
* 提交者将解析更多的合并，并且每个合并更改都在提交中，并带有适当的消息
    * 深入并检查合并提交是不常见的，因此避免合并提交可以确保所有更改在属于它们的地方都有提交

### 什么时候用squash？

"Squashing"是将一系列提交压缩为单个提交的过程。

它在很多情况下都很有用，例如:

- 减少很少或没有上下文的提交(拼写错误更正、格式化、遗忘内容)
- 将单独的更改连接在一起使用时更有意义
- 提交正在重写的工作

### 什么时候避免rebase或者squash？

避免在公共提交或多人工作的共享分支中进行rebase和压制squash。
Rebase和squash重写历史记录并覆盖现有提交，在共享分支上的提交（即，提交到远程存储库或来自其他分支的提交）上执行此操作可能会导致混淆，并且人们可能会丢失其更改（本地和远程） 因为分支和冲突不同。

## 有用的git命令

### rebase -i

使用它来压缩提交、编辑消息、重写/删除/重新排序提交，等等。

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

使用它可以轻松地清理提交，而不需要更复杂的变基(rebase)。[本文](http://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html)提供了很好的示例，说明了如何以及何时执行此操作。

### cherry-pick

在错误的分支上应用您提交的提交非常有用，而无需再次编码。

例如：

```
$ git cherry-pick 790ab21
[master 094d820] Fix English grammar in Contributing
 Date: Sun Feb 25 23:14:23 2018 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### add/checkout/reset [--patch | -p]

假设我们有以下差异:

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

我们可以使用`git add -p`只添加我们想添加的补丁，而不需要更改已经编写的代码。将较大的更改拆分为较小的提交或重置/签出特定的更改是很有用的。

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

## 其他有趣的东西

https://whatthecommit.com/

## 喜欢它？

[Say thanks!](https://saythanks.io/to/RomuloOliveira)

## 贡献

任何形式的帮助将不胜感激。 您可以帮助我的主题示例：

- 语法和拼写更正
- 翻译成其他语言
- 改进源参考
- 信息不正确或不完整

## 灵感，来源和进一步阅读

- [如何编写git提交消息](https://chris.beams.io/posts/git-commit/)
- [Pro Git Book - 提交指南](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
- [关于Git提交消息的说明](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [合并与变基](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Pro Git Book - 改写历史](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)