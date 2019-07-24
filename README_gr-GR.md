# Οδηγός για τα "Μηνύματα Commit"

[![Πείτε ευχαριστώ!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/RomuloOliveira)

Αυτό το κείμενο αποτελεί έναν οδηγό που θα συντελέσει στο να κατανοήσετε την σημασία των μηνυμάτων commit και πώς να τα γράψετε σωστά.

Ενδεχομένως να σας βοηθήσει να μάθετε τι ακριβώς είναι ένα commit, γιατί θεωρείται σημαντικό το να γράφετε καλά μηνύματα, βέλτιστες πρακτικές και κάποιες συμβουλές για το πώς να προσχεδιάσετε και (ξανά)συντάξετε ένα καλό ιστορικό commit.

## Διαθέσιμες Γλώσσες

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
- [Türkçe](README_tr-TR.md)
- [ngôn ngữ tiếng Việt](README_vi-VN.md)
- [繁體中文](README_zh-TW.md)

## Τι είναι ένα "commit"?

Με απλά λόγια, ένα commit είναι ένα _στιγμιότυπο_ των τοπικών σας αρχείων, γραμμένο στο τοπικό σας απωθητήριο(repository).
Αντίθετα με την γνώμη μερικών, [το git δεν αποθηκεύει μόνο την εκάστοτε διαφορά μεταξύ των αρχείων, αποθηκεύει μία πλήρη έκδοση όλων των αρχείων](https://git-scm.com/book/eo/v1/Ekkomenci-Git-Basics#Snapshots,-Not-Differences).
Όσον αφορά τα αρχεία τα οποία δεν άλλαξαν από το ένα commit στο άλλο, το git αποθηκεύει μόνο έναν σύνδεσμο που παραπέμπει στο προηγούμενο, πανομοιότυπο αρχείο που είναι ήδη αποθηκευμένο.

Η παρακάτω εικόνα αναπαριστά τον τρόπο σύμφωνα με τον οποίο το git αποθηκεύει δεδομένα με την πάροδο του χρόνου, όπου κάθε "Εκδοχή" είναι ένα commit:

![](https://i.stack.imgur.com/AQ5TG.png)

## Γιατί είναι τα μηνύματα commit σημαντικά?

- Για να επιταχυνθούν και βελτιστοποιηθούν οι κριτικές κώδικα
- Για να συνδράμουν στην καλύτερη κατανόηση μιας αλλαγής
- Για να εξηγήσουν "τα γιατί (αίτια)" που δεν μπορούν να περιγραφτούν μόνο με την χρήση κώδικα
- Για να βοηθήσουν μελλοντικούς διατηρητές του απωθητηρίου να καταλάβουν γιατί και πώς υλοποιήθηκαν ορισμένες αλλαγές, κάτι που καθιστά την επίλυση προβλημάτων και τον εντοπισμό "bugs" ευκολότερα

Για να επιτύχουμε αυτά τα αποτελέσματα στον μέγιστο βαθμό, μπορούμε να χρησιμοποιήσουμε ορισμένες καλές πρακτικές και πρότυπα που αναλύονται στο επόμενο τμήμα.

## Καλές πρακτικές

Αυτές είναι μερικές πρακτικές που συνέλεξα από τις εμπειρίες μου, άρθρα στο διαδίκτυο, και άλλους οδηγούς. Εάν έχετε άλλες (ή διαφωνείτε με μερικές) νιώστε ευπρόσδεκτοι να ανοίξετε ένα "Pull Request" και να συνεισφέρετε.

### Χρησιμοποιήστε υποτακτική

```
# Καλό
Χρησιμοποιώ InventoryBackendPool για να επανακτήσω inventory backend
```

```
# Κακό
Χρησιμοποίησα InventoryBackendPool για να επανακτήσω inventory backend
```

_Αλλά γιατί να χρησιμοποιήσω υποτακτική;_

Ένα μήνυμα commit περιγράφει τι η αναφερθείσα αλλαγή **κάνει** στην πραγματικότητα, τις επιδράσεις της, όχι τι συνέβη.

[Αυτό το καταπληκτικό άρθρο από τον Chris Beams](https://chris.beams.io/posts/git-commit/) μας παρέχει μία απλή πρόταση που μπορεί να χρησιμοποιηθεί για να μας βοηθήσει να γράψουμε καλύτερα μηνύματα commit στην υποτακτική:

```
Εάν εφαρμοστεί, αυτό το commit θα <μήνυμα commit>
```

Παραδείγματα:

```
# Καλό
Εάν εφαρμοστεί, αυτό το commit θα χρησιμοποιήσει για να επανακτήσει inventory backend
```

```
# Κακό
Εάν εφαρμοστεί, αυτό το commit θα χρησιμοποίησε για να επανακτήσει inventory backend
```

### Κάντε το πρώτο γράμμα κεφαλαίο

```
# Καλό
Προσθέσει την `use` μέθοδο στο Credit μοντέλο
```

```
# Κακό
προσθέσει την `use` μέθοδο στο Credit μοντέλο
```

Ο λόγος για τον οποίο πρέπει να είναι το πρώτο γράμμα κεφαλαίο είναι για να ακολουθηθεί ο κανόνας της γραμματικής που δηλώνει ότι πρέπει να χρησιμοποιούνται κεφαλαία γράμματα στην αρχή των προτάσεων.

Η χρήση αυτής της πρακτικής ενδέχεται να ποικίλλει από άτομο σε άτομο, ομάδα σε ομάδα, ή ακόμα από γλώσσα σε γλώσσα.
Με κεφαλαίο πρώτο γράμμα ή όχι, το σημαντικό είναι να παραμείνετε στο να χρησιμοποιείτε ένα μόνο πρότυπο και να το ακολουθήσετε.

### Προσπαθήστε να επικοινωνήσετε τι κάνει η εκάστοτε αλλαγή χωρίς να απαιτείται αναδρομή στον πηγαίο κώδικα

```
# Καλό
Προσθέσει την `use` μέθοδο στο Credit μοντέλο
```

```
# Κακό
Προσθέσει την `use` μέθοδο
```

```
# Καλό
Αυξήσει το αριστερό κενό μεταξύ του textbox και layout frame
```

```
# Κακό
Προσαρμόσει το css
```

Είναι λυσιτελές σε πολλές εκδοχές (π.χ. πολλαπλά commits, διάφορες αλλαγές και refactors) το να βοηθήσετε τους κριτικούς κώδικα να καταλάβουν τι σκεφτόταν αυτός που διέπραξε τα commits.

### Use the message body to explain "why", "for what", "how" and additional details

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

The subject and the body of the messages are separated by a blank line.
Additional blank lines are considered as a part of the message body.

Characters like `-`, `*` and \` are elements that improve readability.

### Avoid generic messages or messages without any context

```
# Bad
Fix this

Fix stuff

It should work now

Change stuff

Adjust css
```

### Limit the number of characters

[It's recommended](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines) to use a maximum of 50 characters for the subject and 72 for the body.

### Keep language consistency

For project owners: Choose a language and write all commit messages using that language. Ideally, it should match the code comments, default translation locale (for localized projects), etc.

For contributors: Write your commit messages using the same language as the existing commit history.

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

This is a template, [written originally by Tim Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), which appears in the [_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project).

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

This section is a **TL;DR** of Atlassian's excellent tutorial, ["Merging vs. Rebasing"](https://www.atlassian.com/git/tutorials/merging-vs-rebasing).

![](https://wac-cdn.atlassian.com/dam/jcr:01b0b04e-64f3-4659-af21-c4d86bc7cb0b/01.svg?cdnVersion=hq)

### Rebase

**TL;DR:** Applies your branch commits, one by one, upon the base branch, generating a new tree.

![](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=hq)

### Merge

**TL;DR:** Creates a new commit, called (appropriately) a _merge commit_, with the differences between the two branches.

![](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=hq)

### Why do some people prefer to rebase over merge?

I particularly prefer to rebase over merge. The reasons include:

* It generates a "clean" history, without unnecessary merge commits
* _What you see is what you get_, i.e., in a code review all changes come from a specific and entitled commit, avoiding changes hidden in merge commits
* More merges are resolved by the committer, and every merge change is in a commit with a proper message
    * It's unusual to dig in and review merge commits, so avoiding them ensures all changes have a commit where they belong

### When to squash

"Squashing" is the process of taking a series of commits and condensing them into a single commit.

It's useful in several situations, e.g.:

- Reducing commits with little or no context (typo corrections, formatting, forgotten stuff)
- Joining separate changes that make more sense when applied together
- Rewriting _work in progress_ commits

### When to avoid rebase or squash?

Avoid rebase and squash in public commits or in shared branches where multiple people work on.
Rebase and squash rewrite history and overwrite existing commits, doing it on commits that are on shared branches (i.e., commits pushed to a remote repository or that comes from others branches) can cause confusion and people may lose their changes (both locally and remotely) because of divergent trees and conflicts.

## Useful git commands

### rebase -i

Use it to squash commits, edit messages, rewrite/delete/reorder commits, etc.

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

Use it to clean up commits easily and without needing a more complex rebase.
[This article](http://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html) has very good examples of how and when to do it.

### cherry-pick

It is very useful to apply that commit you made on the wrong branch, without the need to code it again.

Example:

```
$ git cherry-pick 790ab21
[master 094d820] Fix English grammar in Contributing
 Date: Sun Feb 25 23:14:23 2018 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### add/checkout/reset [--patch | -p]

Let's say we have the following diff:

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

We can use `git add -p` to add only the patches we want to, without the need to change the code that is already written.
It's useful to split a big change into smaller commits or to reset/checkout specific changes.

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

## Other interesting stuff

- https://whatthecommit.com/
- https://gitmoji.carloscuesta.me/

## Like it?

[Say thanks!](https://saythanks.io/to/RomuloOliveira)

## Contributing

Any kind of help would be appreciated. Example of topics that you can help me with:

- Grammar and spelling corrections
- Translation to other languages
- Improvement of source referencing
- Incorrect or incomplete information

## Inspirations, sources and further reading

- [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
- [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Pro Git Book - Rewriting History](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
