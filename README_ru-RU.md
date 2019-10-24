# Руководство по написанию коммитов

[![Скажи спасибо!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/RomuloOliveira)

Это руководство поможет понять, почему важно писать хорошие сообщения коммитов и как это делать.

Также это руководство может помочь прояснить, что такое коммит, почему важно писать хорошие сообщения, узнать лучшие практики и советы по созданию и (пере)написанию истории коммитов.

## Что такое "коммит"?

Простыми словами, коммит — это _снимок_ ваших локальных файлов, записанный в локальный репозиторий.
Вопреки распространённому мнению, [git хранит не только изменения между файлами, но и в целом полную версию всех файлов](https://git-scm.com/book/ru/v2/%D0%92%D0%B2%D0%B5%D0%B4%D0%B5%D0%BD%D0%B8%D0%B5-%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D1%8B-Git).
Для файлов, которые не менялись от одного коммита к другому, git хранит только ссылку на предыдущий идентичный файл, который уже был сохранен.

На изображении ниже показано, как git хранит данные с течением времени. Каждая "версия" является коммитом:

![](https://i.stack.imgur.com/AQ5TG.png)

## Почему сообщения коммитов важны?

- Чтобы ускорить и упростить проверку кода
- Чтобы помочь в понимании изменений
- Чтобы объяснить вопросы, которые не могут быть описаны только кодом
- Чтобы помочь будущим разработчикам разобраться, почему и как были сделаны изменения, облегчив поиск и устранение ошибок

Чтобы добиться максимального результата, мы можем использовать некоторые полезные практики и стандарты, описанные в следующем разделе.

## Полезные практики

Это некоторые практики, собранные из моего опыта, статей и других руководств. Если у вас есть предложение (или вы не согласны с некоторым) не стесняйтесь открыть пулреквест и внести свой вклад.

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

Сообщение коммита описывает, что конкретно **делают** зафиксированные изменения, его конечный результат, а не что было сделано.

В [замечательной статье Криса Бимса (Chris Beams)](https://chris.beams.io/posts/git-commit/) ([перевод на русский](https://habr.com/ru/post/416887/)) приводится шаблон предложения, который может использоваться, чтобы лучше писать сообщения коммитов в императивной форме:

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

### Начинайте сообщение коммита с заглавной буквы

```
# Хорошо
Add `use` method to Credit model
```

```
# Плохо
add `use` method to Credit model
```

Смысл этой рекомендации простой: в соответствии с правилами грамматики первое слово предложения начинается с заглавной буквы.

Использование этой практики может варьироваться от человека к человеку, от команды к команде или даже от языка к языку.
Заглавная или нет, важно придерживаться единого стандарта и следовать ему.

### Старайтесь описывать изменения так, чтобы указывать на исходный код

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

### Используйте тело сообщения для объяснения "почему", "для чего", "как" и дополнительные детали

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

Тема и описание сообщения разделены пустой строкой.

Дополнительные пустые строки считаются частью описания.

Такие символы как `-`, `*` и ` улучшают общую читаемость.

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

Для участников проекта: Пишите сообщения коммитов на том языке, который используется в истории коммитов.

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

Этот шаблон, [который изначально описан Тимом Поупом (Tim Pope)](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), также упоминается в [_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project).

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

Этот раздел является кратким пересказом превосходного руководства ["Merging vs. Rebasing"](https://www.atlassian.com/git/tutorials/merging-vs-rebasing) от Atlassian.

![](https://wac-cdn.atlassian.com/dam/jcr:01b0b04e-64f3-4659-af21-c4d86bc7cb0b/01.svg?cdnVersion=hq)

### Перебазирование

**Кратко:** Применяет ваши коммиты в ветке, один за другим, к базовой ветки (например, master), генерируя новое дерево.

![](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=hq)

### Слияние

**Кратко:** Создаёт новый коммит, называемый (соответственно) _коммит слияния_ (_merge commit_), с различиями между двумя ветками.

![](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=hq)

### Почему некоторые люди предпочитают перебазирование вместо слияния?

Я, в частности, предпочитаю перебазирование вместо слияния. По следующим причинам:

* Это создает "чистую" историю, без ненужных коммитов-слияний
* _Что видишь, то и имеешь,_, т.е. при ревью кода все изменения идут от определенного коммита, без скрытых изменений в коммитах при слиянии
* Больше слияний решаются автором коммита, поэтому каждое слитое изменение находится в коммите с соответствующим сообщением
    * Обычно не смотрят коммиты-слияния, так что таким образом все изменения зафиксированы в коммите, к которому они непосредственно относятся

### Когда нужно делать объединение коммитов?

Объединение (Squashing) — это процесс объединения множества коммитов в один-единственный коммит.

Это может пригодиться в ряде ситуаций, например:

- Уменьшение количества коммитов с небольшим контекстом или без контекста (исправление опечаток, форматирование, дополнения)
- Объединение независимых изменений, которые лучше всего применять вместе
- Переписывание коммитов в стадии _WIP_ (черновика)

### Когда избегать перебазирования или сжатия?

Избегайте этого в публичных коммитах или в общих ветках, в которых работают несколько человек.
Перебазирование и слияние также перезаписывает историю коммитов и существующие коммиты, делая это с коммитами, которые находятся в разных ветках (например, коммиты, отправленные в удаленный репозиторий или коммиты из других веток) могут вызвать путаницу и поэтому можно потерять изменения (как локальные, так и удаленные) из-за различающегося дерева и конфликтов.

## Полезные команды git

### rebase -i

Используйте их, чтобы объединить коммиты, изменить сообщения, переписать/удалить/изменить порядок коммитов и т.д.

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

Используйте эту команду, чтобы привести в порядок коммиты, не прибегая к перебазированию.
В [этой статье](http://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html) есть хорошие примеры того, как и когда это делать.


### cherry-pick

Эта команда может быть очень полезной для применения коммита, который был сделан в неверной ветке, чтобы не писать код заново.

Пример:

```
$ git cherry-pick 790ab21
[master 094d820] Fix English grammar in Contributing
 Date: Sun Feb 25 23:14:23 2018 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### add/checkout/reset [--patch | -p]

Давайте представим, что у нас есть следующий список различий:

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
 ## Участие в проекте

 Any kind of help would be appreciated. Example of topics that you can help me with:
@@ -202,3 +205,4 @@ Any kind of help would be appreciated. Example of topics that you can help me wi

 - [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
 - [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
+- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
```

Мы можем выполнить `git add -p` чтобы добавить только те патчи, которые нам нужны, без необходимости изменять уже существующий код.
Это очень полезно при разделении больших изменений в маленькие коммиты или для отмены/проверки конкретных изменений.

```
Stage this hunk [y,n,q,a,d,/,j,J,g,s,e,?]? s
Split into 2 hunks.
```

#### часть 1

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

#### часть 2

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

#### часть 3

```diff
@@ -202,3 +205,4 @@ Any kind of help would be appreciated. Example of topics that you can help me wi

 - [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
 - [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
+- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
```

## Кое-что интересное

- https://whatthecommit.com/
- https://gitmoji.carloscuesta.me/

## Нравится это руководство?

[Скажи спасибо!](https://saythanks.io/to/RomuloOliveira)

## Помощь

Любая помощь приветствуется. Вот, например, что вы можете сделать:

- Исправить ошибки в грамматике и правописании
- Перевод на другие языки
- Улучшение списка связанных источников
- Изменить неверную или неполную информацию

## Источники вдохновения и список для дальнейшего чтения

- [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
- [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Pro Git Book - Rewriting History](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
