# Руководство по написанию коммитов

[![Скажи спасибо!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/RomuloOliveira)

Руководство для понимания важности коммитов и как правильно их писать. 

Это может помочь вам понять, что такое коммит, почему важно писать хорошие сообщения, лучшие практики и некоторые советы по планированию и (пере)написанию хорошей истории коммитов.


## Доступные языки

- [Английский](README.md)
- [Португальский](README_pt-BR.md)
- [Немецкий](README_de-DE.md)
- [Испанский](README_es-AR.md)
- [Итальянский](README_it-IT.md)
- [Русский](README_ru-RU.md)

## Что такое "коммит"?

Простыми словами, коммит это _снимок_ ваших локальных файлов, записанный в ваш локальный репозиторий.
Вопреки тому, что думают некоторые, [git хранит не только изменения между файлами, он хранит полную версию всех файлов](https://git-scm.com/book/eo/v1/Ekkomenci-Git-Basics#Snapshots,-Not-Differences).
Для файлов, которые не менялись от одного коммита к другому, git хранит только ссылку на предыдущий идентичный файл, который уже был сохранен.

Изображение ниже показывает, как git хранит данные с течением времени, тогда как каждая "версия" является коммитом:

![](https://i.stack.imgur.com/AQ5TG.png)

## Почему сообщения коммитов важны?

- Чтобы ускорить и упростить проверку кода
- Чтобы помочь в понимании изменений
- Чтобы объяснить вопросы, которые не могут быть описаны только кодом
- Чтобы помочь будущим разработчикам разобраться почему и как были сделаны изменения, облегчив поиск и устранение ошибок

Чтобы добиться максимального результата, мы можем использовать некоторые полезные практики и стандарты, описанные в следующем разделе.

## Полезные практики

Это некоторые практики, собранные из моего опыта, статей и других руководств. Если у вас есть предложение (или вы не согласны с некоторым) не стесняйтесь открыть Pull Request и внести свой вклад.

### Используйте повелительное наклонение

```
# Хорошо
Use InventoryBackendPool to retrieve inventory backend
```

```
# Плохо
Used InventoryBackendPool to retrieve inventory backend
```

_Но зачем использовать повелительное наклонение?_

Сообщения коммита описывает что описанные изменения **делают**, их эффект, а не что было сделано.

[Эта замечательная статья от Chris Beams](https://chris.beams.io/posts/git-commit/) даёт нам простое описание того, что может быть использовано, чтобы лучше писать сообщения коммитов в повелительном наклонении:

```
If applied, this commit will <commit message>
```

Примеры:

```
# Хорошо
If applied, this commit will use InventoryBackendPool to retrieve inventory backend
```

```
# Плохо
If applied, this commit will used InventoryBackendPool to retrieve inventory backend
```

### Используйте заглавную первую букву

```
# Хорошо
Add `use` method to Credit model
```

```
# Плохо
add `use` method to Credit model
```

Причина, по которой первая буква должна быть заглавной, - в следовании грамматическому правилу об использовании заглавных букв в начале предложения.

Использование этой практики может варьироваться от человека к человеку, от команды к команде или даже от языка к языку.
Заглавная или нет, важно придерживаться единому стандарту и следовать ему.

### Попытайтесь сообщить изменения без надобности смотреть исходный код

```
# Хорошо
Add `use` method to Credit model

```

```
# Плохо
Add `use` method
```

```
# Хорошо
Increase left padding between textbox and layout frame
```

```
# Плохо
Adjust css
```

Это полезно во многих случаях (пр. несколько коммитов, различные изменения и рефакторинг), чтобы помочь проверяющим понять о чём думал автор коммита.

### Используйте описание в сообщении для объяснения "почему", "для чего", "как" и дополнительные детали 

```
# Хорошо
Fix method name of InventoryBackend child classes

Classes derived from InventoryBackend were not
respecting the base class interface.

It worked because the cart was calling the backend implementation
incorrectly.
```

```
# Хорошо
Serialize and deserialize credits to json in Cart

Convert the Credit instances to dict for two main reasons:

  - Pickle relies on file path for classes and we do not want to break up
    everything if a refactor is needed
  - Dict and built-in types are pickleable by default
```

```
# Хорошо
Add `use` method to Credit

Change from namedtuple to class because we need to
setup a new attribute (in_use_amount) with a new value
```

Тема и описание сообщения разделены пустой линией.

Дополнительные пустые линии считаются частью описания.

Такие символы как `-`, `*` и \ улучшают общую читаемость.

### Избегайте общих сообщений или сообщений без какого-либо контекста

```
# Плохо
Fix this

Fix stuff

It should work now

Change stuff

Adjust css
```

### Ограничьте длину строк

[Рекомендуется](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines) использовать максимум 50 символов для темы и 72 символа для описания.

### Сохраняйте согласованность языка

Для владельцев проектов: Выберите язык и пишите все сообщения коммитов используя этот язык. В идеале, он должен совпадать с комментариями в коде, стандартным переводом (для переведенных проектов), и т.д.

Для помощников: Пишите ваши сообщения коммитов используя тот же язык, что и в истории коммитов.

```
# Хорошо
ababab Add `use` method to Credit model
efefef Use InventoryBackendPool to retrieve inventory backend
bebebe Fix method name of InventoryBackend child classes
```

```
# Хорошо (Португальский пример)
ababab Adiciona o método `use` ao model Credit
efefef Usa o InventoryBackendPool para recuperar o backend de estoque
bebebe Corrige nome de método na classe InventoryBackend
```

```
# Плохо (смесь Английского и Португальского)
ababab Usa o InventoryBackendPool para recuperar o backend de estoque
efefef Add `use` method to Credit model
cdcdcd Agora vai
```

### Шаблон

Этот шаблон, [который изначально описан Tim Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), также появляется в [_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project).

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

## Перебазировка vs. Слияние

Эта секция является кратким пересказом превосходного руководства Atlassian, ["Merging vs. Rebasing"](https://www.atlassian.com/git/tutorials/merging-vs-rebasing).

![](https://wac-cdn.atlassian.com/dam/jcr:01b0b04e-64f3-4659-af21-c4d86bc7cb0b/01.svg?cdnVersion=hq)

### Перебазировка

**Кратко:** Применяет ваше ответвление коммитов, один за другим, к базовой ветви, генерируя новое дерево. 

![](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=hq)

### Слияние

**Кратко:** Создаёт новый коммит, называемый (соответственно) _слияющим коммитом_ (_merge commit_), с различиями между двумя ветвями.

![](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=hq)

### Почему некоторые люди предпочитают перебазирование вместо слияния?

Я, в частности, предпочитаю перебазирование вместо слияния. По следующим причинам: 

* Это генерирует "чистую" историю, без ненужных слияющих коммитов
* _Что видишь - то и получаешь_, т.е. при обзоре кода все изменения идут от определенного коммита, избегая скрытые изменения в слияющих коммитах 
* Больше слияний решаются автором коммита, и каждое слитое изменение находится в коммите с соответствующим сообщением
    * Это необычно - просматривать слияющие коммиты, поэтому избегая их, вы гарантируете что все изменения имеют коммит, к которому они относятся 

### Когда же "сжимать" коммиты?

Сжатие - это процесс объединения серии коммитов в один коммит. 

Это полезно в нескольких ситуациях, пример:

- Уменьшение количества коммитов с небольшим контекстом или без контекста (исправление ошибок, форматирование, забытые вещи)
- Объединение отдельных изменений, которые имеют больше смысла, когда применяются вместе
- Переписывание _WIP_ (работа в прогрессе) коммитов

### Когда избегать перебазирования или сжатия?

Избегайте этого в публичных коммитах или в общих ветвях, где работают несколько человек.
Это также перезаписывает историю коммитов и существующие коммиты, делая это с коммитами которые находятся в разных ветвях (пр., коммиты отправленные в удаленный репозиторий или которые идут из других веток) могут вызвать путаницу и люди могут потерять их изменения (как локальные, так и удаленные) из-за разрозненного дерева и конфликтов.

## Полезные команды git

### rebase -i

Используйте их чтобы сжать коммиты, изменить сообщения, переписать/удалить/реорганизовать коммиты, и т.д.

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

Используйте для очистки коммитов без необходимости в перебазировке. 
[Данная статья](http://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html) имеет хорошие примеры того, как и когда это делать.

### cherry-pick

Это очень полезно для применения коммитов, которые вы сделали в неправильной ветви, без необходимости писать их заново.

Пример:

```
$ git cherry-pick 790ab21
[master 094d820] Fix English grammar in Contributing
 Date: Sun Feb 25 23:14:23 2018 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### add/checkout/reset [--patch | -p]

Давайте представим что мы имеем следующий список различий:

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

Мы можем использовать `git add -p` чтобы добавить только те патчи, которые нам нужны, без нужды изменять уже написанный код.
Это очень полезно при разделении больших изменений в маленькие коммиты или для отмены/проверки конкретных изменений. 

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

## Другие интересные вещи

https://whatthecommit.com/

## Нравится руководство?

[Скажи спасибо!](https://saythanks.io/to/RomuloOliveira)

## Помощь

Любой вид помощи будет оценен. Пример тем, с которыми вы можете помочь:

- Ошибки в грамматике и правописании 
- Перевод на другие языки
- Улучшение списка связанных источников
- Неверная или неполная информация

## Источники вдохновения и список для дальнейшего чтения

- [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
- [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Pro Git Book - Rewriting History](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)

