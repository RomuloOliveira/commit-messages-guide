#  راهنمای Commit-Message

[![Say Thanks!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/RomuloOliveira)

&#x202b;
راهنمایی برای درک اهمیت Commit-Message و نحوه نوشتن صحیح آن.

&#x202b;
 این راهنما سعی دارد به شما کمک کند یادبگیرید کامیت چیست، چرا نوشتن Commit-Message مناسب مهم است،
تمرین های خوب و نکاتی که می تواند منجرب به بازنگری و داشتن تاریخچه کامیت بهتری شود

## دیگر زبان ها

- [English](README.md)
- [Português](README_pt-BR.md)
- [Deutsch](README_de-DE.md)
- [Español](README_es-AR.md)
- [Italiano](README_it-IT.md)
- [한국어](README_ko-KR.md)
- [Русский](README_ru-RU.md)
- [简体中文](README_zh-CN.md)
- [日本語](README_ja-JP.md)
- [Українська](README_ua-UA.md)
- [پارسی](README_fa-IR.md)

## "Commit" چیست ?

&#x202b;
به زبان ساده، یک کامیت اسنپ شات ی از فایل های محلی شما هست که در مخزن محلی نوشته میشود
برخلاف تصور افراد، [گیت تنها تغییرات فایل هارا نگهداری نمی کند بلکه نسخه کاملی از آنها را نگهداری میکند](https://git-scm.com/book/eo/v1/Ekkomenci-Git-Basics#Snapshots,-Not-Differences).
و برای فایل هایی که تغییری در آنها داده نشده تنها لینک منطبق با فایل موجود را نگهداری میکند.

تصویر زیر نحوه ذخیره اطلاعات درطول زمان را نمایش میدهد، در اینجا هر نسخه یک کامیت محسوب میگردد

![](https://i.stack.imgur.com/AQ5TG.png)

## چرا Commit-Messages اهمیت دارند؟

- سرعت بخشیدن و ساده سازی کدریویو
- کمک به فهم تغییرات
- توضیح "دلیل"، که تنها با کد قابل توضیح نیست
- کمک به نگهداری درآینده و فهم چرا و چگونه تغیرات داده شده اند، عیب یابی و اشکال زدایی سریعتر

برای درک بهتر، چند تمرین و استاندارد در قسمت بعدی توضیح داده خواهد شد

## تمرین خوب

اینها چند تمرین خوب گردآوری شده از تجارب شخصی، اینترنت و سایر راهنماها می باشند، اگه شما با آنها مخالفید یا میتوانید تمرین های بهتر دیگری ارائه دهید میتوانید در توسعه این مخزن مشارکت نمایید

### استفاده از فرم دستوری

```
# Good
Use InventoryBackendPool to retrieve inventory backend
```

```
# Bad
Used InventoryBackendPool to retrieve inventory backend
```

_اما چرا ما شکل دستوری را استفاده میکنیم?_

&#x202b;
یک Commit-Message درواقع آن چیزی راکه تغییرات انجام میدهد یا تاثیر آن را توضیح میدهد نه چیزی که انجام شده است

&#x202b;
[این مقاله جالب توسط Chris Beams](https://chris.beams.io/posts/git-commit/) بوسیله جملات ساده به ما درنوشتن شکل دستوری Commit-Message کمک خواهد کرد:

```
If applied, this commit will <commit message>
```

مثال:

```
# Good
If applied, this commit will use InventoryBackendPool to retrieve inventory backend
```

```
# Bad
If applied, this commit will used InventoryBackendPool to retrieve inventory backend
```

### حرف اول با حروف بزرگ

```
# Good
Add `use` method to Credit model
```

```
# Bad
add `use` method to Credit model
```

دلیل اینکه اولین حرف باید با حروف بزرگ باشد پیروی از قانون گرامر و استفاده از حروف بزرگ در ابتدای جمله می باشد

استفاده از این تمرین از شخصی به شخص دیگر، یا از تیمی به تیمی دیگر یا حتی از زبانی به زبان دیگر متفاوت خواهد بود.
استفاده از حروف بزرگ یا کوچک اهمیتی ندارد، نکته مهم پیروی از یک قانون واحد است

### سعی در رساندن اینکه تغیر چه کاری انجام میدهد بدون نیاز به مشاهده کد 

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

در بسیاری از سناریوها مانند کامیت های متعدد، تغییرات مختلف و بازنویسی به بازبینی کننده کمک خواهد کرد که بفهمد کامیت کننده درچه فکری بوده است 

### استفاده از بدنه Commit-Message برای توضیح "چرا"، "به چه علت"، "چطور" و جزئیات بیشتر

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

&#x202b;
موضوع و بدنه پیام کامیت با یک خط خالی جدا می شوند.
خط های خالی اضافی جزئی از بدنه Commit-Message محسوب خواهند شد

&#x202b;
کارکتر هایی همچون `-`, `*` و `\` باعث تقویت خوانایی Commit-Message خواهند شد

### از متن های کلی یا بی محتوا دوری کنید

```
# Bad
Fix this

Fix stuff

It should work now

Change stuff

Adjust css
```

### تعداد کارکتر های مورد استفاده را محدود کنید

&#x202b;
[توصیه شده](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines) برای موضوع Commit-Message حداکثر 50 کارکتر و برای بدنه آن کداکثر 72 کارکتر استفاده شود.

### در استفاده از زبان نوشتن متن ثابت قدم باشید

&#x202b;
برای مالک پروژه: انتخاب یک زبان و نوشتن همه Commit-Message ها بوسیله آن، که باید همان زبان مورد استفاده برای کامنت ها و زبان پیش فرض برای پروژه های چند زبانه باشد

&#x202b;
برای مشارکت کنندگان: نوشتن Commit-Message با زبان مشابه متن های کامیت قبلی

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

### قالب

&#x202b;
 این یک قالب [نوشته شده توسط Tim Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html) که در [_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project) قابل دسترسی می باشد

```
تغیرات را در حدود ۵۰ کاراکتر یا کمتر خلاصه کنید

متن توضیحات دقیقتر را در ۷۲ کاراکتر بگنجانید،
.اولین خط بعنوان موضوع و مابقی بعنوان بدنه تلقی خواهد شد

یک خط خالی برای جدا کردن موضوع از بدنه ضرروی خواهد بود
در غیراینصورت ابزارهای مختلف مثل `log`, `shortlog`و `rebase` سردرگم خواهند شد

مشکلی که کامیت فوق رفع خواهد کرد را توضیح دهید
برخلاف اینکه چطور تغییرات انجام شده برروی چرا تغییرات رو انجام داده اید
فوکوس کنید.
اینکه تغییرات چطور انجام شده در کد مشخص هست

اینجا مکانی هست که باید توضیح دهید آبا تغیرات تاثیری بر قسمت های مختلف یا عواقب ناخواسته ای خواهند داشت


اگر از ابزاری برای مدیریت ایژوهااستفاده می کنید شماره ارجاع مربوط را در انتهای متن قرار بدید
مثال

Resolves: #123
See also: #456, #789
```
اینجا میتوانید متن اصلی را مشاهده نمایید

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

&#x202b;
این قسمت خلاصه ای از آموزش عالی اطلسین می باشد، ["Merging vs. Rebasing"](https://www.atlassian.com/git/tutorials/merging-vs-rebasing).

![](https://wac-cdn.atlassian.com/dam/jcr:01b0b04e-64f3-4659-af21-c4d86bc7cb0b/01.svg?cdnVersion=hq)

### Rebase

بطور خلاصه قرار دادن کامیت های برنچ شما برروی کامیت های مستر وتولید درخت جدید

![](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=hq)

### Merge

&#x202b;
بطور خلاصه ایجاد یک کامیت جدید بنام _merge commit_ شامل اختلاف دو برنچ

![](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=hq)

### چرا افراد Rebase را به Merge ترجیح میدهند؟

من شخصا ریبیس را به مرج ترجیح میدهم به دلایل زیر

* توسط آن یک تاریخچه کامیت تمیز و بدون کامیت مرج غیرضروری خواهید داشت
* چیزی که شما می بینید چیزی هست که بدست میاورید به این معنی که در بازنگری همه تغییرات در کامیت مربوطه قابل مشاهده هستند وتغییراتی در کامیت مرج مخفی نشده است
* مرجج های بیشتری توسط کامیت کننده برطرف خواهد شد و هر تغییر مرج در کامیتی با متن مناسب خواهد بود
  * در حالت عادی کامیت های مرج بررسی نمیشوند بنابراین اجتناب از آنها این اطمینان به ما خواهد داد که همه تغییرات در کامیت مربوطه خواهند بود
  

### چه وقت از squash استفاده کنیم

&#x202b;
"Squashing" پروسه ای می باشد که یک سری ازکامیت ها به یک کامیت تبدیل خواهند شد
و در وضعیت های مختلفی مفید می باشد مانند

- کاهش تعداد کامیت های بدون محتوا یا کم محتوا مانند اصلاحات تایپی، فرمت کد، چیزهای فراموش شده
- اضافه کردن تغییراتی که درصورت یکی شدن معنی دار خواهند بود
- بازنویسی  کامیت های _work in progress_  

### چه زمانی از rebase یا squash استفاده نکنیم?

در زمانی که برروی برنچ های مشترک یا کامیت های عمومی با سایر افراد کار میکنید  باید از استفاده از آنها اجتناب کنید


این دستورات تاریخچه کامیت ها را بازنویسی همچنین کامیت های موجود رااز بین خواهد برد
در نتیجه انجام آن برروی برنچ های مشترک می تواند باعث ابهام و یا ازدست رفتن تغییرات بدلیل کانفلیک یا انشعابات در درخت کامیت ها گردد 

## دستورات مفید Git

### rebase -i

از این دستور برای ویرایش کامیت، ریبیس، بازنویسی، حذف یا تغییر ترتیب کامیت ها بطور مثال میتوانید استفاده کنید

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

&#x202b;
از این دستور برای پاک سازی آسان بدون نیاز به پیچیدگی های زیاد rebase می توانید استفاده کنید
[این مقاله](http://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html) در بردارنده مثال هایی مفیدی از نحوه و زمان انجام آن می باشد


### cherry-pick
دستور مفیدی برای اضافه کردن کامیتی که در برنچی اشتباهی انجام شده بدون نیاز به کدنویسی مجدد

Example:

```
$ git cherry-pick 790ab21
[master 094d820] Fix English grammar in Contributing
 Date: Sun Feb 25 23:14:23 2018 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### add/checkout/reset [--patch | -p]
بطور مثال ما تفاوت زیر را داریم:

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

&#x202b;
توسط `git add -p` ما میتوانید تنها پچ هایی که میخواهیم اضافه کنیم، 
بدون احتیاج به تغیر کدی که نوشته شده است
همچنین این امکان میسر خواهند بود تغییرات بزرگ به کامیت های کوچکتر شکسته شود یا تغیرات reset/checkout شوند 

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

## سایت های جالب دیگر

- https://whatthecommit.com/
- https://gitmoji.carloscuesta.me/

## مفید بود?

[تشکر !](https://saythanks.io/to/RomuloOliveira)

## مشارکت
از هر نوع کمکی قدردانی خواهد شد بطور مثال در موارد زیر شما میتوانید به بنده کمک کنید

- گرامر و تصحیح املا
- ترجمه به زبان های دیگر
- تقویت منابع و مراجع
- اصلاعات ناقص و نادرست

## منابع الهام گرفته شده و اطلاعات بیشتر

- [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
- [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Pro Git Book - Rewriting History](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
