# Commit Messages Guide

[![Sag danke!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/RomuloOliveira)

Ein Leitfaden, um die Wichtigkeit von Commit-Messages zu verstehen und diese richtig zu formulieren.

Verstehe was ein Commit ist, warum es wichtig ist, eine gute Commit-Message zu schreiben, gute Praxis und ein paar Tipps, um eine saubere Commit-Historie zu planen oder vielleicht sogar nachträglich noch anzupassen.

#### Hinweis des Übersetzers

Auch wenn dies eine Übersetzung darstellen soll, empfiehlt es sich, alle Commit-Messages auf Englisch zu schreiben, deshalb sind die Beispiele nicht übersetzt.

## Was ist ein "Commit"?

Ganz einfach beschrieben ist ein Commit eine Art _Schnappschuss_ deiner lokalen Dateien in deinem Repository (dein Projektordner).
Im Gegensatz zur geläufigen Annahme [speichert Git nicht nur die Unterschiede in den Dateien, sondern immer die gesamte Datei (Quelle auf Englisch)](https://git-scm.com/book/eo/v1/Ekkomenci-Git-Basics#Snapshots,-Not-Differences).
Für Dateien, die sich von einem auf den anderen Commit nicht geändert haben, speichert Git lediglich einen Link zur einer bereits gespeicherten Version in einem vorangegangenen Commit.

Die folgende Grafik zeigt wie Git die Daten mit der Zeit speichert. Jede "Version" meint hier einen Commit.

![](https://i.stack.imgur.com/AQ5TG.png)

## Warum sind Commit-Messages wichtig?

- Um Code-Reviews zu beschleunigen und zu vereinfachen
- Um die erzielte Änderung besser verstehen zu können
- Um _die_ Gründe zu erläutern, die so nicht aus dem Code hervorgehen (Grundsatzentscheidungen)
- Um zukünftigen Entwicklern zu helfen, zu verstehen, wie und warum Änderungen gemacht wurden – was die Fehlersuche und -behebung vereinfacht

Um diese und noch mehr Vorteile möglichst effizient nutzen zu können, sollten wir uns an die folgenden Praktiken und Standards halten.

## Praktiken

Dies sind Praktiken aus meiner eigenen Erfahrung, sowie aus anderen Artikeln/Anleitungen aus dem Internet. Wenn du noch mehr Tipps hast oder manche dieser Praktiken für nicht sinnvoll hältst, beantrage gerne eine Änderung via Pull Request.

### Imperativ verwenden

```
# Good
Use InventoryBackendPool to retrieve inventory backend
```

```
# Bad
Used InventoryBackendPool to retrieve inventory backend
```

_Warum soll ich den Imperativ benutzen?_

Eine Commit-Message beschreibt was die Änderung tatsächlich **tut** – ihre Auswirkungen – nicht was vorher war.

[Dieser sehr gute Artikel von Chris Beams (Quelle auf Englisch)](https://chris.beams.io/posts/git-commit/) gibt uns einen simplen Satzbau vor, dieser hilft dabei bessere Commit-Messages im imperativ zu schreiben:

```
If applied, this commit will: <commit message>
```

Beispiel:

```
# Good
If applied, this commit will use InventoryBackendPool to retrieve inventory backend
```

```
# Bad
If applied, this commit will used InventoryBackendPool to retrieve inventory backend
```

### Große Anfangsbuchstaben

```
# Good
Add `use` method to Credit model
```

```
# Bad
add `use` method to Credit model
```

Diese Regelung ergibt grammatikalisch schlichtweg Sinn, da man den grammatikalischen Regeln bzgl. Großbuchstaben am Satzanfang gerecht wird.

Diese Regelung kann von Entwickler zu Entwickler, Team zu Team oder auch Sprache zu Sprache unterschiedlich sein.

Großschreiben oder nicht, wichtig ist nur, dass man bei einer Variante bleibt.

### Versuche _genau_ zu beschreiben, was die Änderung macht, auch ohne dass man in den Code gucken muss.

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

Dies ist in vielen Situationen (z.B.: mehrere kleine Commits, Refactoring) sinnvoll, um besser zu verstehen, was sich der Entwickler gedacht hat.

### "Warum", "Wozu", "Wie" und andere Details gehören in die Beschreibung der Commit-Message

```
# Good
Fix method name of InventoryBackend child classes

Classes derived from InventoryBackend were not
respecting the base class interface.

It worked because cart was calling the backend implementation
incorrectly.
```

```
# Good
Serialize and deserialize credits to json in Cart

Convert the Credit instances to dict for two main reasons:

  - Pickle relies on file path for classes and we do not want to break up
    everything if a refactor is needed
  - Dict and built-in types are picklable by default
```

```
# Good
Add `use` method to Credit model

Change from namedtuple to class because we need to
setup a new attribute (in_use_amount) with a new value
```

Titel bzw. Betreff der Commit-Message und die Beschreibung müssen mit einer Leerzeile getrennt werden. Alle weiteren Leerzeilen oder Absätze werden als Teil der Beschreibung gewertet.

Trenn- oder Aufzählungszeichen, wie z.B.: `-`, `*` oder `\` verbessern die Lesbarkeit der Beschreibung.

### Vermeide allgemeingültige oder kontextfreie Beschreibungen

```
# Bad
Fix this

Fix stuff

It should work now

Change stuff

Adjust css
```

### Limitiere die Länge der Commit-Message

[Es wird empfohlen (Quelle in ENG)](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines) maximal 50 Zeichen für den Titel/Betreff und 72 Zeichen für die Nachricht zu verwenden.

### Bleibe in einer Sprache

Dies gilt vor allem für Entwickler, für die Englisch nicht die Muttersprache ist. Logischerweise sollte man sich immer dem etablierten Standard anpassen – ganz besonders bei Repositories mit Entwicklern aus vielen verschiedenen Ländern.

Entscheide dich für eine Sprache und bleibe dabei.

```
# Good
ababab Add `use` method to Credit model
efefef Use InventoryBackendPool to retrieve inventory backend
bebebe Fix method name of InventoryBackend child classes
```

```
# Good (German example)
ababab Fügt die `use` Funktion dem Credit Model hinzu
efefef Nutzt den InventoryBackendPool um aufs Bestands-BackEnd zuzugreifen
bebebe Korrigiert den Methodennamen der InventoryBackend Kind-Klassen
```

```
# Bad (mixes English and German)
ababab Fügt die `use` Funktion dem Credit Model hinzu
efefef Add `use` method to Credit model
cdcdcd Fix method name of InventoryBackend child classes
```

### Template

Das folgende Template, [im Original von Tim Pope (Quelle auf Englisch)](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), erschienen so auch in dem Buch [Pro Git Book (Quelle auf Englisch)](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project).

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

## Rebase vs _Merge_

Dieser Abschnitt ist ein **Tl;DR** des lesenswerten Artikels [Atlassian's article Merging vs. Rebasing (Quelle auf Englisch)](https://www.atlassian.com/git/tutorials/merging-vs-rebasing).

![](https://wac-cdn.atlassian.com/dam/jcr:01b0b04e-64f3-4659-af21-c4d86bc7cb0b/01.svg?cdnVersion=hq)

### Rebase

**TL;DR:** Wendet die Änderungen des aktuellen Branches auf den Stand des Basis-Branches an.

![](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=hq)

### _Merge_

**TL;DR:** Erstellt einen neuen Commit, auch _Merge-Commit_, dieser führt die Änderungen beider Branches zusammen.

![](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=hq)

### Warum bevorzugen manche Entwickler rebase?

Ich persönlich bevorzuge rebase. Gründe dafür sind unter anderem:

* Es entsteht eine "saubere" Historie, ohne unnötige Merge-Commits.

* _What you see is what you get_, z.B.: in eine Code-Review sieht man wirklich jeden Commit. Es sind keine Änderungen in Merge-Commits versteckt.
* Jedes Zusammenführen von Code geschieht einzeln durch den Entwickler, so hat jeder Merge einen eigenen Commit mit einer entsprechenen Commit-Message.
    * Im Normalfall werden Merge-Commits in einer Code-Review nicht betrachtet. Hat jede Änderung/Zusammenführung einen eigenen Commit, kann man sicher sein, dass alles an der richtigen Stelle ist und betrachtet werden kann.

### Wann benutzt man squash

Squash beschreibt eine Methode in der eine Reihe von Commits in einem einzelnen Commit zusammengefasst werden.

Hilfreich bei z.B.:

- dem Reduzieren von kleinen/kontextlosen Commits (Rechtschreibfehler, Formatierung, vergessene Änderungen)
- dem Zusammenführen mehrerer Commits, die als Ganzes mehr Sinn ergeben
- dem Neu-Verpacken von _work in progress_ Commits

### Wann sollte man rebase bzw. squash vermeiden

Vermeiden Sie die Verwendung von Rebase und Squash in öffentlichen Commits oder in Branches, in denen mehrere Personen arbeiten.

Rebase und Squash verändern die Historie der Commits und überschreiben bestehende Commits. Verwendet man rebase und squash auf Commits, die sich auf einen gemeinsam genutzten Branch befinden (d.h. Commits, die in ein Remote-Repository verschoben wurden oder von anderen Branches stammen), erzeugt man unötige Verwirrung. Darüber hinaus besteht die Gefahr, dass Andere ihre Änderungen (sowohl lokal als auch auf dem Remote) verlieren, aufgrund von unterschiedlichen Trees und anderen Konflikten.

## Hilfreiche Git Kommandos

### rebase -i

Wird verwendet, um Commits zu squashen, Commit-Messages zu bearbeiten, Neuschreiben/Löschen/Neuordnen von Commits, usw.

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
# s, squash = use commit, but meld into previous commit
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

Wird verwendet, um Commits einfach anzupassen ohne ein komplexes Rebase durchzuführen.
[Dieser Artikel (Quelle auf Englisch)](http://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html) beschreibt mit Beispielen wie und wann man einen fixup durchführt.

### cherry-pick

Sehr hilfreich, wenn man einen Commit der z.B. versehentlich im falschen Branch gepusht wurde, auf den richtigen Branch anwenden will, ohne diesen neuschreiben zu müssen.

Beispiel:

```
$ git cherry-pick 790ab21
[master 094d820] Fix English grammar in Contributing
 Date: Sun Feb 25 23:14:23 2018 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### git add/checkout/reset [--patch | -p]

Angenommen wir haben die folgenden offenen Änderungen:

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
+This is a template, [written originally by Tim Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), which appears in [Pro Git Book](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project).
+
 ## Contributing

 Any kind of help would be appreciated. Example of topics that you can help me with:
@@ -202,3 +205,4 @@ Any kind of help would be appreciated. Example of topics that you can help me wi

 - [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
 - [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
+- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
```

Mit `git add -p` können wir nun ausschließlich die gewünschten Abschnitte zum Commit hinzufügen, ganz ohne dass wir bestehenden Code ändern müssen. Das ist hilfreich, um größere Änderungen in mehrere kleine Commits aufzuteilen oder um ungewollte Änderungen gezielt rückgängig zu machen.

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
+This is a template, [written originally by Tim Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), which appears in [Pro Git Book](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project).
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

## Sonstiges Interessantes

- https://whatthecommit.com/
- https://gitmoji.carloscuesta.me/

## Hat es dir gefallen?

[Sag danke!](https://saythanks.io/to/RomuloOliveira)

## Mitwirken

Jede Art von Hilfe ist willkommen. Zum Beispiel zu den Themen:

- Grammatik und Rechtschreibung
- Übersetzung in andere Sprachen
- Verbesserung der Quell-Referenzen
- Falsche oder unvollständige Information

## Inspiration, Quellen und Lesenswertes

- [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
- [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Pro Git Book - Rewriting History](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
