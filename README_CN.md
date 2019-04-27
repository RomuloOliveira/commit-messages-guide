# 提交信息指南
这是一个了解提交信息重要性和怎么写他们的指南。

它将帮助你了解提交的内容，怎么编写好的提交信息，如果你想写好（重写）提交信息，那么这将展示最佳实践，和一些建议。


## 什么是提交信息


简单来说，提交是本地文件的快照，写在本地存储库中。与某些人的想法相反，[git不仅存储文件之间的差异，而是存储所有文件的完整版本](https://git-scm.com/book/eo/v1/Ekkomenci-Git-Basics#Snapshots,-Not-Differences)。对于未从一次提交更改为另一次提交的文件，git仅存储指向已存储的上一个相同文件的链接。

![](https://camo.githubusercontent.com/461832542a2262717f4cd9e843e8e523a10b83b2/68747470733a2f2f692e737461636b2e696d6775722e636f6d2f41513554472e706e67)

## 为什么提交信息如此重要
- 加快和简化代码审查
- 帮助理解变化
- 解释不能用代码描述的“为什么”
- 为了帮助未来的维护人员弄清楚，你是怎么设计的和如何更改的，使定位问题和调试更容易

为了最大化这些结果，我们可以使用下一节中描述的一些良好实践和标准。

## 好的实践
这些是从我的经验和互联网文章和其他指南中收集的一些实践。如果您有其他的补充（或不同意见），请随时打开Pull Request并提供帮助。

### 使用命令式提交
```
# Good
Use InventoryBackendPool to retrieve inventory backend
```
```
# Bad
Used InventoryBackendPool to retrieve inventory backend
```
*但为什么要使用命令式提交呢？*

提交消息描述的是修改的内容是什么和他的结果，而不是所执行的操作。

[这篇来自Chris Beams的优秀文章](https://chris.beams.io/posts/git-commit/)为我们提供了一个简单的句子，可用于帮助我们以命令式形式编写更好的提交消息：
```
If applied, this commit will <commit message>
```
##### 例子
```
# Good
If applied, this commit will use InventoryBackendPool to retrieve inventory backend
```
```
# Bad
If applied, this commit will used InventoryBackendPool to retrieve inventory backend
```
### 将第一个字母大写
```
# Good
Add `use` method to Credit model
```
```
# Bad
add `use` method to Credit model
```
第一个字母应该大写的原因是遵循在句子开头使用大写字母的语法规则。

这种做法可能因人和团队而异，甚至从语言到语言都有所不同。大不大写，重要的一点是坚持单一标准并遵循它。

### 尝试在不必查看源代码的情况下传达更改的内容

```
# Good
Add `use` method to Credit model
```
```
# Bad
Add `use` method
```
```
# Good
Increase left padding between textbox and layout frame
```
```
# Bad
Adjust css
```
它在许多场景（例如多次提交，多次更改和重构）中非常有用，可以帮助审阅者了解提交者的想法。

### 使用消息正文解释“为什么”，“目标是什么”，“如何做的” 和其他额外细节

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
消息的主题和正文由空行分隔。其他空行当成正文的一部分。

像 - ，*和`这样的字符是提高可读性的元素。

### 避免无意义的描述信息，或没有任何上下文的消息

```
# Bad
Fix this

Fix stuff

It should work now

Change stuff

Adjust css
```

### 限制字符数

[建议](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
最多50个字符用于主题，72个用于内容。

### 保持语言一致性
对于项目所有者：选择一种语言并使用该语言编写所有提交消息。理想情况下，它应匹配代码注释，默认转换区域设置（用于本地化项目）等。

对于贡献者：使用与现有提交历史记录相同的语言编写提交消息。
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

这是一个模板，由Tim Pope编写，出自在Pro Git Book中。

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
### Rebase vs. Merge
这部分是 TL;DR Atlassian优秀教程的，[“Merging vs. Rebasing”](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)。
![](https://camo.githubusercontent.com/100363e5ea3ea688e98a05ff4aad4d491f68ba05/68747470733a2f2f7761632d63646e2e61746c61737369616e2e636f6d2f64616d2f6a63723a30316230623034652d363466332d343635392d616632312d6334643836626337636230622f30312e7376673f63646e56657273696f6e3d6871)

### Rebase
TL; DR：将您的分支提交逐个应用于基本分支，生成新树。
![](https://camo.githubusercontent.com/55a8d4d1514ae2b5f95d2852b907444bdf90c1a2/68747470733a2f2f7761632d63646e2e61746c61737369616e2e636f6d2f64616d2f6a63723a35623135336132322d333862652d343064302d616563382d3566326666666337373165352f30332e7376673f63646e56657273696f6e3d6871)


### Merge
TL; DR：创建一个新的提交，称为（适当地）合并提交，具有两个分支之间的差异。

![](https://camo.githubusercontent.com/5db7f575cb9d38a52d7204353d39ad40b484fcf5/68747470733a2f2f7761632d63646e2e61746c61737369616e2e636f6d2f64616d2f6a63723a65323239666566362d326332662d346134662d623237302d6531653162616139343035352f30322e7376673f63646e56657273696f6e3d6871)

### 为什么人们喜欢rebase
我更喜欢bebase，原因如下

- 它生成一个“干净”的历史记录，没有不必要的合并提交
- 您所看到的就是您所获得的，即在代码审查中，所有更改都来自特定的授权提交，避免了在合并提交中隐藏的更改
- 提交者解决了更多的合并，并且每次合并更改都在提交中并且具有正确的消息
	- 挖掘并审查合并提交是不寻常的，因此避免它们可确保所有更改都具有它们所属的提交

### 什么时候“挤压”

“Squashing”是一系列提交并将它们压缩成一个提交的过程。

它在几种情况下很有用，例如：

- 在很少或没有上下文的情况下减少提交（拼写错误，格式化，遗忘的东西）
- 加入单独的更改，一起应用时更有意义
- 正在重写正在进行的工作

### 什么时候避免rebase或者挤压？
避免在公共提交或多人工作的共享分支中进行rebase和压制。 Rebase和squash重写历史记录并覆盖已有提交记录，在共享分支上的提交（即，提交到远程存储库或来自其他分支的提交）上执行此操作可能会导致混淆，并且人们可能会丢失其更改（本地和远程）因为不同的提交数而产生冲突。

### 有用的git命令
#### rebase -i

用它来压缩提交，编辑消息，重写/删除/重新排序提交等。

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
### fixup

使用它可以轻松清理提交，无需更复杂的rebase。[本文](http://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html)提供了很好的示例，说明了如何以及何时执行此操作。

### cherry-pick
处理在错误的分支上的提交信息非常有用，而无需再次编码。

```
$ git cherry-pick 790ab21
[master 094d820] Fix English grammar in Contributing
 Date: Sun Feb 25 23:14:23 2018 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)

```
 
###  add/checkout/reset [--patch | -p]

假设我们有以下差异：

```
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

### 其他有趣的东西
[https://whatthecommit.com/](https://whatthecommit.com/)












