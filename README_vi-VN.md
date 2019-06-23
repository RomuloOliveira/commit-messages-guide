# Hướng dẫn viết commit

[![Say Thanks!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/RomuloOliveira)

Đây là một bài hướng dấn giúp hiểu được tầm quan trọng của các commit messages và biết cách làm sao để viết chúng cho thật tốt.

Ở bài hướng dẫn này, bạn sẽ hiểu commit là gì, tầm quan trọng của việc viết message tốt cho commit của bạn, những cách thực hành tốt nhất, một số mẹo để lên kế hoạch viết commit và viết/viết lại một lịch sử commit cho tốt.

## "Commit" là gì?

Hãy nghĩ đơn giản, một commit là một _ảnh_ (hoặc bản sao) của những file cục bộ trên kho lưu trữ cá nhân của bạn.
Khác với suy nghĩ của nhiều người, [git không chỉ lưu những khác biệt giữa các phiên bản của file mà lưu trữ toàn bộ các phiên bản](https://git-scm.com/book/eo/v1/Ekkomenci-Git-Basics#Snapshots,-Not-Differences).
Đối với những file không có sự thay đổi so với phiên commit trước, thay vì lưu một file mới, việc git làm đơn giản sẽ là lưu trữ một link trỏ tới file đã được lưu trước đó.

Hình sau mô tả cách mà git lưu trữ dữ liệu theo thời gian, trong đó mỗi một "phiên bản" là một commit:

![](https://i.stack.imgur.com/AQ5TG.png)

## Tại sao những commit message lại quan trọng?

- Làm cho việc đánh giá code trở nên nhanh chóng và hiệu quả hơn.  
- Để giúp người khác hiểu về những sự thay đổi.  
- Để giải thích lý do "tại sao" chỉ giải thích bằng code là chưa đủ mà còn phải thêm bằng message.  
- Để sau này, những người bảo trì project có thể tìm ra lý do tại sao lại có những thay đổi và chúng được thực hiện như thế nào, điều này làm cho việc khắc phục sự cố cũng như gở lỗi trở nên dễ dàng hơn.

Để hiểu thêm về những điểm trên, chúng ta có thể sử dụng các good practices(tạm hiểu là những cách làm tốt, được rút ra từ kinh nghiệm, Tiếng Việt không có từ ngữ tương ứng nên người dịch sẽ giữ nguyên từ này) và những tiêu chuẩn được mô tả bên dưới.

## Good Practices

Đây là những cách làm tốt mà tác giả thu thập từ kinh nghiệp thực tế, bài báo trên internet cũng như như một số bài hướng dẫn khác. Nếu thấy có sai sót hoặc muốn thêm ví dụ vui lòng mở một Pull Request và tham gia đóng góp.  

### Dùng thể mệnh lệnh(imperative form)

```
# Good
Use InventoryBackendPool to retrieve inventory backend
```

```
# Bad
Used InventoryBackendPool to retrieve inventory backend
```

_Nhưng tại sao phải dùng thể mệnh lệnh?_

Một commit message mô tả các thay đổi này thực sự **làm** những gì, tác động của nó, chứ không phải nói về những việc đã được thực hiện.

[Bài báo tuyệt vời của Chris Beams](https://chris.beams.io/posts/git-commit/) cung cúp cho chúng ta một mẫu câu đơn giản mà ta có thể dùng, giúp chúng ta viết commit message tốt hơn ở thể mệnh lệnh:

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

### Viết hoa chữ cái đầu

```
# Good
Add `use` method to Credit model
```

```
# Bad
add `use` method to Credit model
```

Lý do là chúng ta phải tuân theo luật ngữ pháp về việc viết hoa chữ cái đầu tiên của câu.

Việc sử dụng practice này có thể khác nhau tùy từng người, từng team, hoặc giữa các ngôn ngữ.
Viết hoa hay không thì điều quan trọng là phải tuân theo một tiêu chuẩn duy nhất, không được đan xen tùy lúc.  

### Cố gắng truyền đạt những gì thay đổi gây ra mà không cần phải xem mã nguồn.

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

Việc này rất hữu ích trong nhiều tình huống (Ví dụ: Nhiều commit, có một vài thay đổi và cấu trúc lại) để giúp những người đánh giá có thể hiểu người commit đã nghĩ gì.

### Sử dụng phần thân của message để giải thích "tại sao", "để làm gì", "như thế nào" và một số chi tiết bổ sung

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

Phần tiêu đề và phần thân của message phải được ngăn ra bởi một dòng trống. Những dòng trống phía dưới dòng trống đó(nếu có) sẽ được xem như thuộc phần thân của message.  

Những kí tự như `-`, `*` và \` là những yếu tố message dễ đọc hơn.

### Tránh những message có nội dung chung chung hoặc những message mà không hề có bối cảnh  

```
# Bad
Fix this

Fix stuff

It should work now

Change stuff

Adjust css
```

### Giới hạn số lượng chữ cái.

[Bạn nên](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines) sử dụng tối đa 50 ký tự cho phần chủ đề và 72 ký tự mỗi dòng cho phần thân message.  

### Có sự nhất quán trong việc sử dụng ngôn ngữ

Đối với chủ dự dán: Chọn một ngôn ngữ và viết mọi commit message bằng ngôn ngữ đó. Choose a language and write all commit messages using that language. Lý tưởng nhất là ngôn ngữ dùng cho commit message phải khớp với các code comment, ngôn ngữ dịch mặc định (đối với những dự án được bản địa hóa), v.v...

Đối với những người tham gia đóng góp: Viết commit message bằng ngôn ngữ tương tự ngôn ngữ của các commit message trước đó.  

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

### Commit message mẫu

Đây là mẫu commit message, [được viết ban đầu bởi Tim Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html) và xuất hiện trong cuốn [_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project).

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

Việc dịch nội dung này theo người dịch là không cần thiết, tuy nhiên để những bạn mới tập làm quen hiểu rõ hơn thì người dịch sẽ cung cấp thêm bản dịch của mẫu trên:

```
Tóm tắt những thay đổi trong 50 ký tự hoặc ít hơn

Thêm những giải thích nếu cần thiết, khoảng 72 chữ một dòng. Trong một 
số bối cảnh, dòng đầu tiên được xem là tiêu đề và phần còn lại chính là
nội dung. Dòng trống phân tách giữa tiêu đề và phần thân rất quan trọng
, trừ khi bạn không viết phần thân; nhiều công cụ như `log`, `shortlog`
và `rebase` có thể bối rối nếu bạn không để dòng trống ở giữa.

Giải thích vấn đề mà phiên commit này giải quyết. Tập trung vào lý do 
tại sao lại thay đổi thay vì giải thích cách thức thay đổi - How (code 
của ta sẽ giải thích how). Có tác dụng phụ hay hậu quả (có chứng cứ) 
của những những thay đổi này không?  Đây là nơi chúng ta giải thích 
chúng.

Các đoạn tiếp theo cũng sẽ đúng sau một dòng trống.

 - Các bullet point được chấp nhận.

 - Các bullet point thường thấy là các dấu gạch đầu dòng và các dấu hoa
  thị. Trước các bullet point là một khoảng trắng, giữa các ý là một 
  dòng trống. Tuy nhiên chỗ này sẽ có một số quy ước khác nhau.

Nếu bạn sử dụng trình theo dõi vấn đề (issue tracker), Đặt tham chiếu 
đến chúng ở dưới cùng, như thế này:

Giải quyết: #123
Xem thêm: #456, #789
```

## Rebase vs. Merge

Chương này là một [**TL;DR**](https://en.wikipedia.org/wiki/Wikipedia:Too_long;_didn%27t_read)(bản tóm tắt ngắn gọn) của bài hướng dẫn tuyệt vời của Atlassian, ["Merging vs. Rebasing"](https://www.atlassian.com/git/tutorials/merging-vs-rebasing).

![](https://wac-cdn.atlassian.com/dam/jcr:01b0b04e-64f3-4659-af21-c4d86bc7cb0b/01.svg?cdnVersion=hq)

Ở đây người dịch sẽ không dịch từ rebase và merge sang Tiếng Việt để tránh gây bối rối cũng như tiện cho người đọc tìm hiểu keyword sau này.

### Rebase

**TL;DR:** Gắn các commit trên nhánh của bạn, từng cái một, lên branch gốc, tạo ra một cây mới.

![](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=hq)

### Merge

**TL;DR:** tạo một commit mới, gọi là(một cách thích hợp) một _merge commit_, chứa tất cả những sự khác nhau giữa 2 branch.

![](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=hq)

### Tại sao một số người thích rebase hơn merge?

Tác giả đặc biệt thích rebase hơn merge. Có những lý do sau:

* Nó sinh ra một lịch sử "sạch", không có những merge commit không cần thiết.  
* _Bạn thấy gì bạn sẽ nhận cái đó_, i.e., trong lúc đánh giá code,ta sẽ thấy được mọi thay đổi từ các commit cụ thể và có tên, tránh những thay đổi ẩn nằm trong các merge commits.  
* Nhiều merges được giải quyết bởi người commit hơn, và mỗi một sự thay đổi do merge gây ra sẽ nằm commit với message phù hợp.  
 * Thông thường ta sẽ không khai thác cũng như đánh giá những merge commit, vì thế tránh chúng để đảm bảo mọi thay đổi điều có commit chứa thay đổi đó.

### Khi nào cần squash

"Squashing" là quá trình lấy một dãy commit và ép lại thành một commit duy nhất.

Sẽ rất hữu ích trong một vài tình huống, ví dụ:

- Giảm những commits ít hoặc không có ngữ cảnh (sửa lỗi chính tả, định dạng, nội dung bị quên)
- Kết hợp những sự thay đổi riêng biệt, những thay đổi này có ý nghĩa hơn khi áp dụng cùng nhau.
- Viết lại những commit kiểu _công việc đang tiếng hành_.

### Khi nào nên tránh rebase hoặc squash?

Tránh rebase và squash ở những commit công khai hoặc những nhánh đồng sở hữu nơi nhiều người cùng làm việc trên nhánh đó.
Rebase và squashy viết lại history và ghi đè lên các commit hiện có, thực hiện nó trên những commit trên những nhánh đồng sở hữu (ví dụ, commit được đẩy đến một kho lưu trữ từ xa hoặc đến từ những nhánh khác) có thể gây bối rối và mọi người có thể mất những thay đổi của họ (cục bộ lẫn từ xa) bởi những cây phân nhánh và xung đột(divergent trees and conflicts).  

## Những git command hữu ích

### rebase -i

Sử dụng để squash những commit, sửa messages, viết lại/xóa/sắp xếp lại những commit, v,v...

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

Sử dụng để dọn dẹp các commit một cách dễ dàng và không cần rebase phức tạp.
[Bài báo này](http://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html) có những ví dục tốt về cách thức cũng như khi nào thì nên sử dụng fixup.

### cherry-pick

`cherry-pick` Khi bạn commit sai nhánh, sử dụng cherry-pick để lấy một commit trên nhánh sai và áp dụng vào nhánh mình muốn, thay vì phải code lại từ đầu.

Ví dụ:

```
$ git cherry-pick 790ab21
[master 094d820] Fix English grammar in Contributing
 Date: Sun Feb 25 23:14:23 2018 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### add/checkout/reset [--patch | -p]

Tưởng tượng chúng ta có những sự khác biệt sau:

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

Chúng ta có thể dùng `git add -p` để thêm duy nhất chỗ mà ta muốn, không cần phải thay đổi code đã được viết.
Sẽ hữu ích khi chia một thay đổi lớn thành những commit nhỏ hơn hoặc reset/checkout một thay đổi cụ thể.

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

## Những thứ thú vị khác có thể tham khảo:

- https://whatthecommit.com/
- https://gitmoji.carloscuesta.me/

## Thích tài liệu này?

[Gởi lời cảm ơn tới RomuloOliveira!](https://saythanks.io/to/RomuloOliveira)

## Đóng góp

Mọi sự đóng góp nào điều được đánh giá cao. Ví dụ về những chủ đề mà bạn có thể giúp:

- Sửa lỗi ngữ pháp và lỗi chính tả  
- Dịch sang ngôn ngữ khác  
- Cải thiện nguồn tham khảo  
- Sửa các thông tin không chính xác hoặc không đầy đủ  

## Nguồn cảm hứng, nguồn và đọc thêm:

- [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
- [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Pro Git Book - Rewriting History](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
