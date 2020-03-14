# Керівництво по написанню комітів

[![Скажи дякую!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/RomuloOliveira)

Керівництво для розуміння важливості повідомлень комітів і того, як правильно їх писати.

Це може допомогти вам зрозуміти, що таке коміт, чому важливо писати хороші повідомлення, кращі практики і деякі поради по плануванню і (пере)написанню хорошої історії комітів.

## Що таке "коміт"?

Простими словами, коміт - це _знімок(зліпок)_ ваших локальних файлів, записаний в локальний репозиторій.
Насправді, [git зберігає не тільки зміни між файлами, але і в цілому повну версію всіх файлів](https://git-scm.com/book/ru/v2/%D0%92%D0%B2%D0%B5%D0%B4%D0%B5%D0%BD%D0%B8%D0%B5-%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D1%8B-Git).
Для файлів, які не змінювались від одного коміта до іншого, git зберігає тільки посилання на попередній ідентичний файл, котрий вже був збережений.

Зображення нижче показує, як git зберігає дані з плином часу, тоді як кожна "версія" являється комітом:

![](https://i.stack.imgur.com/AQ5TG.png)

## Чому повідомлення комітів важливі?

- Щоб прискорити і спростити перевірку коду
- Щоб допомогти в розумінні змін
- Щоб прояснити речі, які не можуть бути описані тільки кодом
- Щоб допомогти майбутнім розробникам розібратись, чому і як були зроблені зміни, полегшивши пошук і ліквідацію помилок

Щоб досягнути максимального результату, ми можем використовувати деякі корисні практики та стандарти, описанні в наступному розділі.

## Корисні практики

Це деякі практики, зібрані з мого досвіду, статей та решти керівництв. Якщо у вас є пропозиція (або ви не згідні з деякими речами) не соромтесь відкрити пулреквест і внести свій внесок.

### Використовуйте наказовий спосіб

```
# Добре
Use InventoryBackendPool to retrieve inventory backend
```

```
# Погано
Used InventoryBackendPool to retrieve inventory backend
```

_Але навіщо використовувати наказовий спосіб?_

Повідомлення коміту описує, що конкретно **роблять** зафіксовані зміни, його кінцевий результат, а не що було зроблено.

В [чудовій статті Кріса Бімса (Chris Beams)](https://chris.beams.io/posts/git-commit/) ([російський переклад](https://habr.com/ru/post/416887/)) приводиться шаблон пропозиції, який може використовуватись, щоб краще писати сповіщення комітів в імперативній формі:

```
If applied, this commit will <commit message>
```

Приклади:

```
# Добре
If applied, this commit will use InventoryBackendPool to retrieve inventory backend
```

```
# Погано
If applied, this commit will used InventoryBackendPool to retrieve inventory backend
```

### Починайте повідомлення коміту з Великої букви

```
# Добре
Add `use` method to Credit model
```

```
# Погано
add `use` method to Credit model
```

Зміст цієї рекомендації простий: відповідно до правил граматики перше слово у реченні починається з великої букви.

Використання цієї практики може варіюватись від людини до людини, від команди до команди або рідше від мови до мови.
Велика чи ні, важливо дотримуватись єдиного стандарту і слідувати йому.

### Старайтесь описувати зміни так, щоб вказувати на сирцевий код, тобто місце де сталася зміна

```
# Добре
Add `use` method to Credit model

```

```
# Погано
Add `use` method
```

```
# Добре
Increase left padding between textbox and layout frame
```

```
# Погано
Adjust css
```

Це корисно в багатьох випадках (пр. декілька комітів, різноманітні зміни і рефакторинг), щоб допомогти рев'юверам зрозуміти про що думав автор коміту, та що мав на увазі, коли писав повідомлення.

### Використовуйте тіло повідомлення для пояснення "чому", "для чого", "як" та додаткові деталі

```
# Добре
Fix method name of InventoryBackend child classes

Classes derived from InventoryBackend were not
respecting the base class interface.

It worked because the cart was calling the backend implementation
incorrectly.
```

```
# Добре
Serialize and deserialize credits to json in Cart

Convert the Credit instances to dict for two main reasons:

  - Pickle relies on file path for classes and we do not want to break up
    everything if a refactor is needed
  - Dict and built-in types are pickleable by default
```

```
# Добре
Add `use` method to Credit

Change from namedtuple to class because we need to
setup a new attribute (in_use_amount) with a new value
```

Тема і опис повідомлення розділені пустою стрічкою.

Додаткові пусті стрічки рахуються частиною опису.

Такі символи як `-`, `*` і ` покращують загальну читаємість.

### Запобігайте появі загальних повідомлень або повідомлень без будь-якого контексту

```
# Погано
Fix this

Fix stuff

It should work now

Change stuff

Adjust css
```

### Обмежте довжину стрічок

[Рекомендуеться](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines) використовувати максимум 50 символів для теми і 72 символа для опису.

### Зберігайте узгодженість мовлення

Для власників проектів: Оберіть мову та пишіть всі повідомлення комітів використовуючи цю мову. В ідеалі, він має співпадати з коментарями в коді, стандартним перекладом (для перекладених проектів), і т.д.

Для учасників проекту: Пишіть повідомлення комітів тією мовою, котра використовується в історії комітів.

```
# Добре
ababab Add `use` method to Credit model
efefef Use InventoryBackendPool to retrieve inventory backend
bebebe Fix method name of InventoryBackend child classes
```

```
# Добре (Португальський приклад)
ababab Adiciona o método `use` ao model Credit
efefef Usa o InventoryBackendPool para recuperar o backend de estoque
bebebe Corrige nome de método na classe InventoryBackend
```

```
# Погано (суміш Англійської та Португальської)
ababab Usa o InventoryBackendPool para recuperar o backend de estoque
efefef Add `use` method to Credit model
cdcdcd Agora vai
```

### Шаблон

Цей шаблон, [ був з самого початку описаний Тімом Поупом (Tim Pope)](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), також згадується в [_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project).

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

## Перебазування (Rebase) vs. Злиття (Merging)

Цей розділ є коротким переказом чудового керівництва ["Merging vs. Rebasing"](https://www.atlassian.com/git/tutorials/merging-vs-rebasing) від Atlassian.

![](https://wac-cdn.atlassian.com/dam/jcr:01b0b04e-64f3-4659-af21-c4d86bc7cb0b/01.svg?cdnVersion=hq)

### Перебазування(Rebase)

**Коротко:** Застосовує ваші коміти в гілці, один за другим, до базової гілки (наприклад, master), генеруючи нове дерево.

![](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=hq)

### Злиття (Merging)

**Коротко:** Створює новий коміт, названий (відповідним чином) _коміт злиття_ (_merge commit_), з різницею між двома гілками.

![](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=hq)

### Чому деякі люди надають перевагу перебазуванню замість злиття?

Я, особисто, надаю перевагу перебазуванню замість злиття. З наступних причин:

* Це створює "чисту" історію, без непотрібних комітів-злиттів
* _Що бачиш, те і маєш,_, т.е. при рев'ю коду всі зміни йдуть від певного коміту, без прихованих змін в комітах при злитті
* Всі конфлікти при злитті вирішуються автором коміту, тому кожна злита зміна знаходиться в коміті з відповідним повідомленням
    * Зазвичай не дивляться на коміти-злиття, так що таким образом всі зміни зафіксовані в коміті, до якого вони безпосередньо відносяться

### Коли необхідно робити об'єднання комітів?

Об'єднання (Squashing) — це процес об'єднання декількох комітів в один-єдиний коміт.

Це може знадобитися в ряді ситуацій, наприклад:

- Зменшення кількості комітів з невеликим контекстом або без контексту (виправлення опечатків, форматування, доповнення)
- Об'єднання незалежних змін, котрі краще за все застосовувати разом
- Переписування комітів в стадії _WIP_ (чорновика)

### Коли уникати перебазування або об'єднання (squash)?

Уникайте цього в публічних комітах або в загальних гілках, в яких працюють кілька людей.
Перебазування і об'єднання також перезаписує історію комітів і існуючі коміти, роблячи це з комітів, які знаходяться в різних гілках (наприклад, комітів, що відправлені в віддалений репозиторій або комітів з інших гілок) що може викликати плутанину і тому можна втратити зміни (як локальні, так і віддалені) через різницю дерева і конфліктів.

## Корисні команди git

### rebase -i

Використовуйте їх, щоб об'єднати коміти, змінити повідомлення, переписати / видалити / змінити порядок комітів і т.д.

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

Використовуйте цю команду, щоб привести в порядок коміти, не використовуючи перебазування.
В [цій статті](http://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html) є гарні приклади того, як і коли це робити.


### cherry-pick

Ця команда може бути дуже корисною для зміни коміту, який був зроблений в неправильній гілці, щоб не писати код заново.

Приклад:

```
$ git cherry-pick 790ab21
[master 094d820] Fix English grammar in Contributing
 Date: Sun Feb 25 23:14:23 2018 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### add/checkout/reset [--patch | -p]

Давайте уявимо, що у нас є наступний список відмінностей:

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
 ## Участь у проекті

 Any kind of help would be appreciated. Example of topics that you can help me with:
@@ -202,3 +205,4 @@ Any kind of help would be appreciated. Example of topics that you can help me wi

 - [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
 - [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
+- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
```

Ми можемо виконати `git add -p` щоб додати тільки ті патчі, які нам потрібні, без необхідності змінювати вже існуючий код.
Це дуже корисно при розділенні великих змін в маленькі коміти або для відміни/перевірки конкретних змін.

```
Stage this hunk [y,n,q,a,d,/,j,J,g,s,e,?]? s
Split into 2 hunks.
```

#### частина 1

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

#### частина 2

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

#### частина 3

```diff
@@ -202,3 +205,4 @@ Any kind of help would be appreciated. Example of topics that you can help me wi

 - [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
 - [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
+- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
```

## Дещо цікаве

- https://whatthecommit.com/
- https://gitmoji.carloscuesta.me/

## Подобається це керівництво?

[Скажи Дякую!](https://saythanks.io/to/RomuloOliveira)

## Допомога

Люба допомога вітається. Ось, наприклад, Що ви можете зробити:

- Виправити помилки в граматиці та правописі
- Переклад на інші мови
- Покращення списку пов'язаних джерел
- Змінити неправильну або неповну інформацію

## Джерела натхнення та список для подальшого читання

- [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
- [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Pro Git Book - Rewriting History](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
