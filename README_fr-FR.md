# Guide sur les messages de commit

[![Dites merci!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/RomuloOliveira)

Un guide pour comprendre l'importance des messages de commit et comment bien les écrire.

Cela pourrait vous aider à comprendre ce qu'un commit est, pourquoi c'est important de bien écrire ses messages, les meilleurs techniques et quelques astuces, pour mieux (ré)écrire une bonne "commit history"

## Qu'est-ce qu'un "commit" ?

Dans des termes simples, un commit est une _sauvegarde_ de vos fichiers locaux, écrits dans votre dépôt local.
Contrairement à ce que certaines personnes pensent, [git ne stocke pas seulement la différence entre ces fichiers, il stocke une version complète de tous les fichiers](https://git-scm.com/book/eo/v1/Ekkomenci-Git-Basics#Snapshots,-Not-Differences).
Pour les fichiers qui ne changent pas d'un commit à l'autre, git stocke juste un lien vers la version précédente identique qui est déjà stockée.

L'image ci-dessous montre comment git stocke les fichiers à travers le temps, dans quelle "Version" est un commit.

![](https://i.stack.imgur.com/AQ5TG.png)

## Pourquoi les messages de commit sont importants ?

- Pour raccourcir et faciliter les revues de code.
- Pour aider dans la compréhension d'un changement.
- Pour expliquer les "pourquoi", qui ne sauraient être décris en code
- Pour aider les futurs personnes qui vont devoir maintenir le code à comprendre les différents changements, et l'évolution du code.

Pour maximiser ces résultats, nous pouvons utiliser certaines bonnes pratiques et des standards, décrits dans la prochaine section.

## Bons usages

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

_Pourquoi l'impératif ?_

Un message de commit décrit ce que le changement **fait**, ces effets, pas ce qui à été fait.

[Cet excellent article de Chris Beams](https://chris.beams.io/posts/git-commit/)
Nous donne une phrase simple qui peut être utilisée pour mieux écrire les messages de commit à l'impératif.

```
If applied, this commit will <commit message>
```

Exemples:

```
# Bon
If applied, this commit will use InventoryBackendPool to retrieve inventory backend
```

```
# Mauvais
If applied, this commit will used InventoryBackendPool to retrieve inventory backend
```

### Mettre une majuscule au début de la phrase

```
# Bon
Add `use` method to Credit model
```

```
# Mauvais
add `use` method to Credit model
```

On met la première lettre en majuscule pour suivre la règle de grammaire selon laquelle on doit utiliser une majuscule au début d'une phrase.

Cette pratique peut être ou non appliquée en fonction des personnes, des équipes ou même des languages. Dans tous les cas, l'important est de définir une règle et de s'y tenir.

### Essayer de décrire les changements sans avoir à lire le code

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

Cela est utile dans de nombreux scenarios (commits multiples, beaucoup changements et refactorisations) pour aider les reviewers à comprendre ce à quoi la personne qui a fait le commit pensait.

### Use the message body to explain "why", "for what", "how" and additional details
### Utiliser le corps du message pour expliquer "pourquoi", pour "quoi", "comment" et autres détails

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

L'objet et le corps du message sont séparés par un saut de ligne.
Des sauts de ligne additionels sont considérés comme faisant partie du corps.
Eviter les caractères tels que `-`, `*` et `\` améliore la lisiblité.

### Eviter les messages génériques ou sans aucun contexte

```
# Mauvais
Fix this

Fix stuff

It should work now

Change stuff

Adjust css
```

### Limiter le nombre de colonnes

[Il est recommandé](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines) d'utiliser un maximum de 50 caractères pour le sujet, et 72 pour le corps.

### Garder la cohérence linguistique

Pour les propriétaires de projet: Choisissez une langue et écrivez tous les messages de validation en utilisant cette langue. Idéalement, il devrait correspondre aux commentaires de code, aux paramètres régionaux de traduction par défaut (pour les projets localisés), etc.

Pour les contributeurs: Écrivez vos messages de validation en utilisant la même langue que l'historique de validation existant.


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

C'est un modèle, [écrit par Tim Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), qui apparait dans le  [_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project).

```
Résumer les changements en 50 caractères ou moins.

Texte explicatif plus détaillé, si nécessaire. Mettez un retour à la ligne à environ 72 caractères. Dans certains contextes, la première ligne est traitée
en tant que sujet du commit et le reste en tant que corps. La ligne
vide séparant le sommaire du corps est critique (sauf si vous omettez complètement le corps); certains outils tels que `log`, `shortlog` et
`rebase` peuvent être confus si vous les fusionnez ensemble.

Expliquez le problème que ce commit est en train de résoudre. Concentrez-vous sur
les raisons pour lesquelles vous apportez ce changement, par opposition à la
façon dont (le code explique cela).
Est-ce qu'il y at-il des effets secondaires ou d’autres conséquences non intuitives de ce changement? Voici l'endroit pour les expliquer.

Les autres paragraphes viennent après les lignes vides.

 - Les puces sont ok.

 - Généralement, un tiret ou un astérisque est utilisé pour la puce, précédé d'un espace, avec des lignes vides entre les deux, mais les conventions varient ici.

Si vous utilisez un outil de suivi des problèmes,
mettez les références à la fin comme ceci:

Resolves: #123
Voir aussi: #456, #789
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
* Ce que vous voyez est ce que vous obtenez, c’est-à-dire que dans une revue de code, toutes les modifications proviennent d’un commit spécifique, évitant les changements masqués dans les commits de merge.
* Plus de merges sont résolus par la personne qui commit, et chaque modification de merge est dans un commit avec un message propre à celui-ci.
* Il est inhabituel de chercher et d'examiner les commits de merge. Evitez-les donc pour vous assurer que tous les changements ont un commit auquel ils appartiennent.

### Quand "squash"

"Squashing" est le processus consistant à prendre une série de commits et à les condenser en un seul commit.

C'est utile dans plusieurs situations, e.g.:

- Réduire le nombre de commit avec peu ou pas de contexte (correction de fautes d'orthographe, formatage, choses oubliées)
- Joindre des modifications distinctes qui ont plus de sens lorsqu'elles sont appliquées ensemble
- Réécrire les commits de _travail en cours_

### Quand éviter rebase ou squash ?

Il faut éviter rebase et squash dans les commits publiques ou dans les branches partagées où plusieurs personnes travaillent dessus.
Rebase et squash réécrivent l'historique et écrasent les commits existants, le faire sur des commits qui sont dans des branches partagées (i.e., les commits push sur le dépôt distant ou qui viennent d'autres branches) peut entrainer de la confusion, et les gens risquent de perdre leurs changements (autant localement que à distance) car les arbres et les conflicts divergent.

## Commandes git pratiques

### rebase -i

Utilisez-la pour squash les commits, modifier les messages, réécrire/supprimer/réorganiser les commits, etc.


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

Utilisez-la pour nettoyer les commits facilement et sans nécessiter de rebase plus complexe.
[Cet article](http://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html) a de bons exemples de comment et quand le faire.

### cherry-pick

C'est très utile pour appliquer le commit que vous avez fait sur la mauvaise branche, sans qu'il soit nécessaire de le coder à nouveau.

Exemple:

```
$ git cherry-pick 790ab21
[master 094d820] Fix English grammar in Contributing
 Date: Sun Feb 25 23:14:23 2018 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### add/checkout/reset [--patch | -p]

Imaginons que nous avons le diff suivant:

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

On peut utiliser git add -p pour ajouter uniquement les correctifs que nous voulons, sans qu'il soit nécessaire de modifier le code déjà écrit.
Il est utile de scinder un gros changement en de plus petits commits ou de réinitialiser/extraire des modifications spécifiques.

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

- https://whatthecommit.com/
- https://gitmoji.carloscuesta.me/

## Vous aimez ?

[Dites merci!](https://saythanks.io/to/RomuloOliveira)

## Contribuer

Toute sorte d'aide est appréciée. Voici quelques exemples de sujets où vous pouvez m'aider :

- Corrections grammaticales et orthographiques
- Traduction dans d'autres langues
- Meilleures référencement des sources
- Informations incorrectes ou incompletes

## Inspirations, sources et lectures complémentaires:

- [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
- [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Pro Git Book - Rewriting History](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
