# Hướng dẫn commit message

[![Say Thanks!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/RomuloOliveira)

Hướng dẫn này giúp ta hiểu được tầm quan trọng của commit message và cách viết chúng.

Nó giúp bạn biết được commit là gì, tại sao viết một message thì quan trọng, các ví dụ thực tiễn và vài mẹo để lập kế hoạch và viết lại một commit history tốt.

# "Commit" là gì?

Nói một cách đơn giản, commit là một snapshot của các local file, được viết trong local repository.
Trái với suy nghĩ của một số người, [git không chỉ lưu trữ sự khác biệt giữa các file, nó còn lưu trữ full version của tất cả các file](https://git-scm.com/book/eo/v1/Ekkomenci-Git-Basics#Snapshots,-Not-Differences).
Đối với các file không có sự thay đổi từ commit này sang commit khác, git chỉ lưu trữ một liên kết tới file giống hệt trước đó đã được lưu.

Hình ảnh bên dưới cho thấy cách git lưu trữ dữ liệu theo thời gian, trong đó mỗi "Version" là một commit:

![](https://i.stack.imgur.com/AQ5TG.png)

# Tại sao commit message thì quan trọng

- Để tăng tốc và hợp lý hóa các code review
- Để giúp hiểu về sự thay đổi
- Để giải thích "the whys", cái mà không thể được mô tả chỉ bằng code
- Để giúp các maintainer trong tương lai tìm ra lý do và cách thức các thay đổi được thực hiện, giúp khắc phục sự cố và debug dễ dàng hơn

Để tối đa hóa các kết quả đó, chúng ta có thể sử dụng một số ví dụ thực tiễn được mô tả trong phần tiếp theo.

## Ví dụ thực tiễn

Đây là một số ví dụ thực tiễn được thu thập từ kinh nghiệm của tôi, bài viết trên internet và các hướng dẫn khác. Nếu bạn có không đồng ý với một số thứ, vui lòng mở Pull Request và đóng góp.

### Dùng dạng câu mệnh lệnh

```
# Good
Use InventoryBackendPool to retrieve inventory backend
```

```
# Bad
Used InventoryBackendPool to retrieve inventory backend
```

_Nhưng tại sao lại dùng câu mệnh lệnh_

Một commit message mô tả những cái thay đổi được tham chiếu đến việc **thực hiện ở hiện tại**, những tác động của nó, chứ không phải những cái đã được thực hiện.

[Bài viết tuyệt vời này đến từ Chris Beams](https://chris.beams.io/posts/git-commit/) cung cấp cho chúng ta một câu đơn giản có thể được sử dụng để giúp chúng ta viết commit message tốt hơn ở dạng mệnh lệnh:

```
If applied, this commit will <commit message>
```

Ví dụ:

```
# Good
If applied, this commit will use InventoryBackendPool to retrieve inventory backend
```

```
# Bad
If applied, this commit will used InventoryBackendPool to retrieve inventory backend
```

### Viết hoa chữ cái đầu tiên

```
# Good
Add `use` method to Credit model
```

```
# Bad
add `use` method to Credit model
```

Lý do mà chữ cái đầu tiên nên được viết hoa là tuân theo quy tắc ngữ pháp sử dụng chữ in hoa ở đầu câu.

Việc sử dụng chữ cái in hoa ở đầu câu có khác nhau với mỗi người, mỗi team hoặc thậm chí giữa ngôn ngữ này với ngôn ngữ khác.
Viết hoa hay không, một điểm quan trọng là tuân theo một tiêu chuẩn duy nhất và theo sát nó.

### Cố gắng truyền đạt được những gì thay đổi mà không cần phải nhìn vào source code

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

Nó rất hữu ích trong nhiều tình huống (ví dụ: nhiều lần commit, một số thay đổi và refactor) để giúp reviewer hiểu người được những gì commiter đang nghĩ.

### Sử dụng phần thân message để giải thích "why", "for what", "how" và các chi tiết bổ sung

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

Chủ đề và phần thân message được phân tách bằng một dòng trống. 
Các dòng trống bổ sung được coi là một phần của nội dung message.

Các ký tự như `-`, `*` và \` là các phần tử để giúp việc đọc message dễ hơn.

### Tránh viết các message chung chung mà không có bất kỳ ngữ cảnh nào

```
# Bad
Fix this

Fix stuff

It should work now

Change stuff

Adjust css
```

### Giới hạn số lượng ký tự

[Người ta khuyến khích](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines) sử dụng tối đa 50 ký tự cho chủ đề và 72 ký tự cho phần thân message.

### Ngôn ngữ phải nhất quán

Đố với các project owner: Chọn một ngôn ngữ và viết tất cả các commit message bằng ngôn ngữ đó. Hợp lý nhất là nó phải phù hợp với các code comment, ngôn ngữ dịch mặc định (đối với các dự án được bản địa hóa), v.v.

Đối với các contributor: Viết commit message chung với ngôn ngữ tồn tại trong commit history.

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

### Template

Đây là một template, [được viết bởi Tim Pope](ttp://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), xuất hiện trong [_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project).

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

## Rebase và Merge

Phần này là một phần trong các hướng dẫn của Atlassian, ["Merging vs. Rebasing"](https://www.atlassian.com/git/tutorials/merging-vs-rebasing).

![](https://wac-cdn.atlassian.com/dam/jcr:01b0b04e-64f3-4659-af21-c4d86bc7cb0b/01.svg?cdnVersion=hq)

### Rebase

Apply các commit trong branch của bạn, từng cái một, vào sau branch cơ sở, tạo ra một tree mới.

![](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=hq)

### Merge

Tạo một commit mới, được gọi là _merge commit_, với sự khác biệt giữa hai branch.

![](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=hq)

## Vì sao một số người thích rebase hơn merge?

Tôi đặc biệt thích rebase hơn merge vì một số lý do sau:

- Nó tạo ra một history "sạch", không có các merge commit không cần thiết
- Những gì bạn thấy là những gì bạn nhận được, tức là, trong code review, tất cả các thay đổi đều đến từ một commit cụ thể và được cho phép, để tránh các thay đổi ẩn trong merge commit
- Thực hiện merge nhiều được giải quyết bởi committer, và mỗi sự thay đổi do merge đều nằm trong một commit với một message phù hợp
    - Việc khai thác và xem xét các merge commit là không thông dụng, vì vậy hãy tránh chúng để đảm bảo tất cả các thay đổi đều có commit đúng nơi thuộc về chúng

### Khi nào "squash"

"Squashing" là quá trình thực hiện một loạt các commit và cô đọng chúng thành một commit duy nhất.

Nó hữu ích trong một số tình huống, ví dụ:

- Giảm các commit mà có ít hoặc không có ngữ cảnh (như sửa lỗi chính tả, định dạng, nội dung bị quên)
- Hợp nhất các thay đổi rời rạc có ý nghĩa khi apply chúng cùng nhau
- Viết lại công việc commit đang tiến hành

### Khi nào cần tránh rebase hoặc squash?

Cần tránh rebase và squash trong commit công khai hoặc trong các branch được chia sẻ, nơi mà có nhiều người làm việc cùng nhau. 
Rebase và squash viết lại history và ghi đè các commit đang tồn tại, thực hiện nó trên các commit trên các branch được chia sẻ (nghĩa là các commit được push đến một remote repository hoặc đến từ các branch khác) có thể gây ra nhầm lẫn và mọi người có thể bị mất các thay đổi của họ (cả trên local và remote) bởi vì các tree bất đồng nhau và các xung đột.

## Các git command hữu ích

### rebase -i

Sử dụng nó để squash commit, sửa các message, viết lại/xóa/sắp xếp lại các commit, v.v.

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

Sử dụng nó để dọn dẹp các commit dễ dàng hơn và không cần một rebase phức tạp hơn. 
[Bài viết này](http://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html) có các ví dụ rất hay về cách thức và thời điểm thực hiện nó.

### cherry-pick

Nó rất hữu ích để apply commit mà bạn đã thực hiện trên branch sai, mà không cần phải code lại.

Ví dụ:

```
$ git cherry-pick 790ab21
[master 094d820] Fix English grammar in Contributing
 Date: Sun Feb 25 23:14:23 2018 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### add/checkout/reset [--patch | -p]

Hãy theo dõi diff dưới đây:

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

Chúng ta có thể sử dụng `git add -p` để chỉ thêm các bản vá mà chúng ta muốn, mà không cần phải thay đổi code đã được viết.
Thật hữu ích khi chia một thay đổi lớn thành các commit nhỏ hơn hoặc reset/checkout các thay đổi cụ thể.

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

## Giới thiệu các chủ đề thú vị khác

- https://whatthecommit.com/
- https://gitmoji.carloscuesta.me/

## Like it?

[Say thanks!](https://saythanks.io/to/RomuloOliveira)

## Đóng góp

Bất kỳ hình thức trợ giúp nào cũng được đánh giá cao. Ví dụ về các chủ đề mà bạn có thể giúp tôi:

- Sửa lỗi ngữ pháp và chính tả
- Dịch sang các ngôn ngữ khác
- Cải thiện nguồn tham khảo
- Thông tin không chính xác hoặc không đầy đủ

## Nguồn tham khảo và đọc thêm

- [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
- [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Pro Git Book - Rewriting History](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
