# Guide sur les messages de commit

[![Dites merci!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/RomuloOliveira)

Un guide pour comprendre l'importance des messages de commit et comment bien les écrire.

Cela pourrait vous aider à comprendre ce qu'un commit est, pourquoi c'est important de bien écrire ses messages, les meilleurs techniques et quelques astuces, pour mieux (ré)écrire une bonne "commit history" 

## Langages Disponibles

- [English](README.md)
- [Português](README_pt-BR.md)
- [Deutsch](README_de-DE.md)
- [Français](README_fr-FR.md)
## Qu'est-ce qu'un "commit" ?

Dans des termes simples, un commit est une _sauvegarde_ de vos fichiers local, écrits dans votre repository local.
Contrairement à ce que certaines personnes pensent, [git ne stockent pas seulement la différence entre ces fichiers, il stock une version complète de tous les fichiers](https://git-scm.com/book/eo/v1/Ekkomenci-Git-Basics#Snapshots,-Not-Differences).
For les fichiers qui ne changent pas d'un commit à l'autre, git stock just un lien vers la version précédente identique qui est déjà stockée.

L'image ci-dessous montre comment git stock les fichiers à travers le temps, dans quelle "Version" est un commit.


![](https://i.stack.imgur.com/AQ5TG.png)

## Pourquoi les messages de commit sont importants ?

- Pour raccourcir et faciliter les code-review
- Pour aider dans la compréhension d'un changement.
- Pour expliquer les "pourquoi", qui ne sauraient être décris en code
- Pour aider les futurs personnes qui vont devoir maintenir le code à comprendre les différents changements, et l'évolution du code.

Pour maximiser ces résultats, nous pouvons utiliser certaines bonnes pratiques et des standards, décrits dans la prochaine section.

## Bons Usages

Il y a quelques bons usages recueillit par l'experience, des articles sur internet, et d'autres guides. Si vous en avez d'autres (ou n'êtes pas d'accord avec certains), soyez libres d'ouvrir une demande de Pull et de contribuer à l'amélioration du guide.

### Utilisez l'impératif

```
# Bon
Use InventoryBackendPool to retrieve inventory backend
```

```
# Mauvais 
Used InventoryBackendPool to retrieve inventory backend
```

_Pourquoi l'impératif ?__

Un message de commit décrit ce que le changement **fait**, ces effets, pas ce qui à été fait.

[Cet excelent article de Chris Beams](https://chris.beams.io/posts/git-commit/)
Nous donne une phrase simple qui peut être utilisée pour mieux écrire les messages de commit à l'impératif.

```
If applied, this commit will <commit message>
```

Examples:

```
# Bon
If applied, this commit will use InventoryBackendPool to retrieve inventory backend
```

```
# Mauvais
If applied, this commit will used InventoryBackendPool to retrieve inventory backend
```

### Capitalize the first letter

```
# Bon
Add `use` method to Credit model
```

```
# Mauvais
add `use` method to Credit model
```

The reason that the first letter should be capitalized is to follow the grammar rule of using capital letters at the beginning of sentences.

The use of this practice may vary from person to person, team to team, or even from language to language.
Capitalized or not, an important point is to stick to a single standard and follow it.

### Try to communicate what the change does without having to look at the source code

```
# Bon
Add `use` method to Credit model

```

```
# Mauvais
Add `use` method
```

```
# Bon
Increase left padding between textbox and layout frame
```

```
# Mauvais
Adjust css
```

It is useful in many scenarios (e.g. multiple commits, several changes and refactors) to help reviewers understand what the committer was thinking.

### Use the message body to explain "why", "for what", "how" and additional details

```
# Bon
Fix method name of InventoryBackend child classes

Classes derived from InventoryBackend were not
respecting the base class interface.

It worked because cart was calling the backend implementation
incorrectly.
```

```
# Bon
Serialize and deserialize credits to json in Cart

Convert the Credit instances to dict for two main reasons:

  - Pickle relies on file path for classes and we do not want to break up
    everything if a refactor is needed
  - Dict and built-in types are picklable by default
```

```
# Bon
Add `use` method to Credit

Change from namedtuple to class because we need to
setup a new attribute (in_use_amount) with a new value
```

The subject and the body of the messages are separated by a blank line.
Additional blank lines are considered as a part of the message body.

Characters like `-`, `*` and \` are elements that improve readability.

### Avoid generic messages or messages without any context

```
# Mauvais
Fix this

Fix stuff

It should work now

Change stuff

Adjust css
```

### Limit the number of columns

[It's recommended](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines) to use a maximum of 50 characters for the subject and 72 for the body.

### Keep language consistency

For project owners: Choose a language and write all commit messages using that language. Ideally it should match the code comments, default translation locale (for localized projects), etc.

For contributors: Write your commit messages using the same language as the existing commit history.

```
# Bon
ababab Add `use` method to Credit model
efefef Use InventoryBackendPool to retrieve inventory backend
bebebe Fix method name of InventoryBackend child classes
```

```
# Bon (Exemple Portugais)
ababab Adiciona o método `use` ao model Credit
efefef Usa o InventoryBackendPool para recuperar o backend de estoque
bebebe Corrige nome de método na classe InventoryBackend
```

```
# Bad (mix Anglais et Portugais)
ababab Usa o InventoryBackendPool para recuperar o backend de estoque
efefef Add `use` method to Credit model
cdcdcd Agora vai
```

### Modèle

C'est un modèle, [Créé par Tim Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), qui apparait dans le  [_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project).

```
Résumer les changement en 50 charactères ou moins.

Les textes plus détaillées, si nécéssaires, peuvent être plus ou moins
de 72 charactères. Dans certains contextes, la première ligne est traitée
en tant que sujet du commit et le rest en tant que corps. La ligne
blanche séparrant le sommaire du corps est critique (sauf si il n'y a
pas de corps du tout); certains outils tels que `log`, `shortlog` et
`rebase` peuvent être confus si vous les lancez ensemble.

Expliquez le problème que le commit résout. Concentrez vous sur
"pourquoi" vous faites ce changement contrairement à "comment"
(le code explique déjà cela).
Est-ce qu'il y a des effets ou d'autres conséquences qui ne sont
pas intuitives concernant ce changement ? C'est l'endroit où vous
pouvez les décrire.

Les autres paragraphes viennent après des lignes vides.

 - Les puces sont ok.

 - Vous pouvez utilisez des astérisques et des puces, tout en gardant
   une syntaxe correcte.

Si vous utilisez un outil de suivi des problèmes,
mettez des références à la fin comme ceci:

Resolves: #123
See also: #456, #789
```

## Rebase vs. Merge

Cette section est un **TL;DR** de l'excellent tutoriel d'Atlassian, ["Merging vs. Rebasing"](https://www.atlassian.com/git/tutorials/merging-vs-rebasing).

![](https://wac-cdn.atlassian.com/dam/jcr:01b0b04e-64f3-4659-af21-c4d86bc7cb0b/01.svg?cdnVersion=hq)

### Rebase

**TL;DR:** Applique vos commits de branche, un par un, sur la branche principale, générant un nouvel "arbre"

![](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=hq)

### Merge

**TL;DR:** Créé un nouveau commit, appelé un _merge commit_, avec les différences entre ces deux branches.

![](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=hq)

### Pourquoi certaines personnes préfères rebase plutôt que merge ?

Je préfère particulièrement rebase plutôt que merge. Les raisons sont:

* Cela génère un historique "propre", sans merge commits inutiles.
* _Ce que vous voyez est ce que avez_, i.e., dans une code review tout les changements viennent d'un commit spécifique, empéchant les changements cachés dans les merge commits
* Plus de merges sont résolus par la personne qui commit, et chaque merge change est dans un commit avec un message propre à celui-ci.
    * Ce n'est pas commun de chercher et d'examiner les merge commits, donc les éviter assure que tous les changements ont un commit où ils sont.

### Quand "squash"

"Squasher" c'est prendre une série de commits et les condensser dans un seul commit.

C'est utile dans plusieurs situations, e.g.:

- Réduire le nombre de commit avec peu ou pas de contexte (correction de fautes d'orthographe, formatage, choses oubliées)
- Regrouper des changements séparés, qui ont plus de sens une fois regroupés.
- Réécrire les commits de _travail en cours_

### Quand éviter rebase ou squash ?

Il faut éviter rebase et squash dans les commits publiques ou dans les branches partagées où plusieurs personnes travaillent dessus.

Rebase et squash réécrivent l'history and écrasent less commits existants, le faire sur des commits qui sont dans des branches partagées (i.e., les commits push sur le remote repository ou qui viennent d'autres branches) peut entrainer de la confusion, et les gens risquent de perdre leurs changements (autant localement que remotely) car les arbres et les conflicts divergent.

## Commandes git pratiques

### rebase -i

Utilise là to squash les commits, editer les messages, réécrire/supprimer/réorganiser les commits, etc.

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

#### fixup

Utilise là to nettoyer les commits facilement et sans avoir besoin d'un rebase plus complexe.
[Cet article](http://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html) a de bons exemples de comment et quand le faire.

### cherry-pick

C'est très utile pour appliquer des commits étant fais sur la mauvaise branche, sans avoir besoin de le recoder. 

Example:

```
$ git cherry-pick 790ab21
[master 094d820] Fix English grammar in Contributing
 Date: Sun Feb 25 23:14:23 2018 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### add/checkout/reset [--patch | -p]

Immaginons que nous avons le diff suivant:

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

+### Modèle
+
+C'est un modèle, [Ecrit par Tim Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), qui apparait dans [_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project).
+
 ## Contribuer

 Toute sorte d'aide est apréciée. Voici quelques exemples de sujets où vous pouvez m'aider. 

@@ -202,3 +205,4 @@ Toute sorte d'aide est apréciée. Voici quelques exemples de sujets où vous pouvez m'aider. 

 - [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
 - [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
+- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
```

Ont peut utiliser 'git add -p' pour ajouter seulement les patch que nous souhaitons, sans le besoin de changer le code qui est déjà écrit.
C'est utile de séparer un gros changement en plusieurs commits ou de reset/checkout certains changements spécifiques.

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

## D'autres choses intéréssantes

https://whatthecommit.com/

## Vous aimez ?

[Dites merci!](https://saythanks.io/to/RomuloOliveira)

## Prendre Part
Toute sorte d'aide est apréciée. Voici quelques exemples de sujets où vous pouvez m'aider :

- Grammaire et correction orthopgraphique
- Traduction dans d'autres langues
- Meilleures référencement des sources
- Informations incorrectes ou incompletes

## Inspirations, sources et d'autre choses à lire :

- [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
- [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Pro Git Book - Rewriting History](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
