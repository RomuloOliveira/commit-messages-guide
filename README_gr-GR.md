# Οδηγός για τα "Μηνύματα Commit"

[![Πείτε ευχαριστώ!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/RomuloOliveira)

Αυτό το κείμενο αποτελεί έναν οδηγό που θα συντελέσει στο να κατανοήσετε την σημασία των μηνυμάτων commit και πώς να τα γράψετε σωστά.

Ενδεχομένως να σας βοηθήσει να μάθετε τι ακριβώς είναι ένα commit, γιατί θεωρείται σημαντικό το να γράφετε καλά μηνύματα, βέλτιστες πρακτικές και κάποιες συμβουλές για το πώς να προσχεδιάσετε και (ξανά)συντάξετε ένα καλό ιστορικό commit.

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

### Χρησιμοποιήστε το σώμα κειμένου για να εξηγήσετε "γιατί", "για ποιον σκοπό", "πώς" και επιπρόσθετες λεπτομέρειες

```
# Καλό
Φτιάξει όνομα μεθόδου των παιδιών κλάσεων του InventoryBackend

Οι κλάσεις που εξήγοντο από το InventoryBackend δεν
σέβοταν το βασικό interface της κλάσης.

Δούλεψε επειδή το cart καλούσε την υλοποίηση
backend με λάθος τρόπο.
```

```
# Καλό
Μετατρέψει τα credits σε σειριακά και αντίστροφα ως json στο Cart

Μετατροπή των Credit instances σε dict για δύο κύριους λόγους:

  - Το Pickle στηρίζεται στο file path για τις κλάσεις και δεν θέλουμε να
    χαλάσουμε τα πάντα εφ' όσον χρειαστεί ένα refactor
  - Το dict και οι ενσωματομένοι τύποι είναι δυνατόν να γίνουν
    pickled από μόνοι τους
```

```
# Καλό
Προσθέσει την `use` μέθοδο στο Credit

Αλλαγή από namedtuple σε κλάση γιατί χρειαζόμαστε να
εγκατασταστήσουμε ένα καινούργιο attribute (in_use_amount)
με μία νέα τιμή
```

Το θέμα και το σώμα των κειμένων διαχωρίζονται μέσω μίας κενής γραμμής.
Περαιτέρω κενές γραμμές εκλαμβάνονται ως μέρος του σώματος κειμένου.

Χαρακτήρες όπως `-`, `*` και \` είναι στοιχεία που βελτιώνουν την αναγνωσιμότητα.

### Αποφύγετε γενικού ύφους μηνύματα ή μηνύματα χωρίς κάποιο γενικό πλαίσιο

```
# Κακό
Φτιάξει αυτό

Φτιάξει πράγματα

Τώρα πρέπει να δουλέψει

Αλλάξει πράγματα

Τροποποιήσει το css
```

### Περιορίστε τον αριθμό των χαρακτήρων

[Προτείνεται](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines) να χρησιμοποιείτε ένα μέγιστο 50 χαρακτήρων για το θέμα και 72 για το σώμα του κειμένου

### Διατηρήστε συνοχή στην γλώσσα

Για τους ιδιοκτήτες project: Διαλέξτε μία γλώσσα και γράψτε όλα τα μηνύματα commit χρησιμοποιώντας αυτήν την γλώσσα. Ιδανικά, θα πρέπει να ταιριάζει με τα σχόλια στον κώδικα, το προκαθορισμένο locale μετάφρασης (για projects τοπικού χαρακτήρα), κτλ.

Για όσους συνεισφέρουν: Γράψτε τα μηνύματα commit σας χρησιμοποιώντας την ίδια γλώσσα που χρησιμοποιείται στο ήδη υπάρχον ιστορικό commit.

```
# Καλό
ababab Προσθέσει την `use` μέθοδο στο μοντέλο Credit
efefef Χρησιμοποιήσει το InventoryBackendPool για να επανακτήσει το inventory backend
bebebe Διορθώσει το όνομα των μεθόδων των InventoryBackend παιδιών κλάσεων
```

```
# Καλό (Παράδειγμα στα Πορτογαλικά)
ababab Adiciona o método `use` ao model Credit
efefef Usa o InventoryBackendPool para recuperar o backend de estoque
bebebe Corrige nome de método na classe InventoryBackend
```

```
# Κακό (Μπλέκει Αγγλικά και Πορτογαλικά)
ababab Usa o InventoryBackendPool para recuperar o backend de estoque
efefef Add `use` method to Credit model
cdcdcd Agora vai
```

### Πρότυπο

Αυτό είναι ένα πρότυπο, [που αρχικά έγραψε ο Tim Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), το οποίο εμφανίζεται στο [_Pro Git Βιβλίο_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project).

```
Αναφέρετε περιληπτικά τις αλλαγές σε περίπου 50 χαρακτήρες ή λιγότερους

Πιο λεπτομερές επεξηγηματικό κείμενο, εάν κρίνεται απαραίτητο.
Συμπυκνώστε το σε περίπου 72 χαρακτήρες. Εντός κάποιων πλαισίων,
η πρώτη γραμμή αντιμετωπίζεται ως το θέμα του commit και το υπόλοιπο
του κειμένου ως το σώμα του. Η κενή γραμμή που διαχωρίζει την
περίληψη από το σώμα είναι ζωτικής σημασίας (εκτός και αν παραλείψετε
το σώμα εντελώς); ποικίλια εργαλεία όπως τα `log`, `shortlog` και `rebase`
μπορεί να μπερδευτούν αν τρέξετε τα δύο μαζί.

Εξηγήστε το πρόβλημα που επιλύει αυτό το commit. Εστιάστε στο γιατί
κάνετε αυτήν την αλλαγή αντί στο πώς (ο κώδικας το εξηγεί αυτό).
Υπάρχουν έμμεσες επιδράσεις ή άλλες μη διαισθητικές συνέπειες αυτής
της αλλαγής; Εδώ είναι το μέρος για να τις εξηγήσετε.

Περαιτέρω παράγραφοι έρχονται μετά από κενές γραμμές.

  - Τα bullet points είναι, και αυτά, εντάξει

  - Συνήθως για το bullet χρησιμοποιείται μία παύλα ή ένας αστερίσκος,
    μετά από ένα μόνο κενό, με κενές γραμμές ανάμεσα, αλλά οι συμβάσεις
    σχετικά με αυτό το θέμα ποικίλουν.

Άμα χρησιμοποιείτε έναν issue tracker, τοποθετήστε αναφορές σε αυτούς
στο κάτω μέρος, όπως έτσι:

Επιλύει: #123
Δείτε επίσης: #456, #789
```

## Rebase εναντίον Merge

Αυτό το τμήμα είναι ένα **TL;DR** του εξαιρετικού tutorial του Atlassian, ["Merging εναντίον Rebasing"](https://www.atlassian.com/git/tutorials/merging-vs-rebasing).

![](https://wac-cdn.atlassian.com/dam/jcr:01b0b04e-64f3-4659-af21-c4d86bc7cb0b/01.svg?cdnVersion=hq)

### Rebase

**TL;DR:** Εφαρμόζει τα commits στο κλαδί που είστε, ένα ένα, στο κλαδί βάση, παράγοντας ένα καινούργιο δέντρο.

![](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=hq)

### Merge

**TL;DR:** Δημιουργεί ένα νέο commit, το επονομαζόμενο (δικαίως) _merge commit_, με τις διαφορές μεταξύ των δύο κλαδιών.

![](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=hq)

### Γιατί μερικοί προτιμούν να κάνουν rebase αντί για merge;

Εγώ προσωπικά προτιμώ να κάνω rebase αντί για merge. Οι λόγοι περιλαμβάνουν:

* Παράγει ένα "καθαρό" ιστορικό, χωρίς αχρείαστα merge commits
* _Ότι δείτε είναι ότι παίρνετε_, δηλαδή, σε μια κριτική κώδικα όλες οι αλλαγές προέρχονται από ένα συγκεκριμένο και ονοματιζμένο commit, αποφεύγοντας αλλαγές κρυμμένες μέσα σε merge commits
* Περισσότερα merges επιλύονται από αυτόν που κάνει commit, και κάθε αλλαγή merge είναι σε ένα commit με ένα κατάλληλο μήνυμα
    * Είναι ασηνύθιστο να ψάχνεις και να κάνεις κριτική κώδικα σε merge commits, οπότε το να τα αποφεύγεις διασφαλίζει το ότι όλες οι αλλαγές έχουν ένα commit στο οποίο ανήκουν
I particularly prefer to rebase over merge. The reasons include:

### Πότε να κάνετε squash

"Squashing" είναι η διαδικασία του να παίρνεις μια ακολουθία από commits και μετά να τις συμπυκνώνεις σε ένα μόνο commit.

Είναι χρήσιμο σε πληθώρα περιστάσεων, π.χ:

- Ελλάτωση commits με λίγο ή καθόλου πλαίσιο (διορθώσεις τυπογραφικών λαθών, formatting, ξεχασμένα πράγματα)
- Σύντμηση διαφορετικών αλλαγών που βγάζουν περισσότερο νόημα όταν εφαρμοστούν μαζί
- Γράψιμο έτη μία φορά _work in progress_ commits

### Πότε να αποφύγετε το rebase ή το squash;

Αποφύγετε τα rebase και squash σε δημόσια commits ή σε κοινόχρηστα κλαδιά όπου δουλεύουν πολλοί άνθρωποι.
Το rebase και το squash ξανά γράφουν το ιστορικό και γράφονται επί των ήδη υπαρχόντων commits, το να τα κάνετε σε commits που είναι σε κοινόχρηστα κλαδιά (δηλαδή, commits που έχετε κάνει push σε remote απωθητήριο ή που προέρχονται από κλαδιά άλλων) μπορεί να προκαλέσει σύγχηση και ενδέχεται άνθρωποι να χάσουν τις αλλαγές τους (και τοπικά και remotely) λόγω των αποκλίνοντων δέντρων και conflicts.

## Χρήσιμες εντολές git

### rebase -i

Χρησιμοποιήστε την για να κάνετε squash commits, να επεξεργαστείτε μηνύματα, να ξαναγράψετε/διαγράψετε/αναταξινομήσετε commits, κλπ.

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

Χρησιμοποιήστε την για να καθαρίσετε commits εύκολα και χωρίς να χρειαστεί ένα πιο πολύπλοκο rebase.
[Αυτό το άρθρο](http://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html) περιέχει πολύ καλά παραδείγματα σχετικλα με το πώς και πότε να το κάνετε.

### cherry-pick

Είναι πολύ χρήσιμη για να εφαρμόσετε το commit που κάνατε στο λάθος κλαδί, χωρίς την ανάγκη να ξαναγράψετε τον κώδικα.

Παράδειγμα:
```
$ git cherry-pick 790ab21
[master 094d820] Φτιάξει ελληνική γραμματική στο "Συνεισφορά"
 Date: Sun Feb 25 23:14:23 2018 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### add/checkout/reset [--patch | -p]

Ας υποθέσουμε ότι έχουμε το ακόλουθο diff:

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

Μπορούμε να χρησιμοποιήσουμε `git add -p` για να προσθέσουμε μόνο τα patches που θέλουμε, χωρίς να χρειάζεται να αλλάξουμε τον κώδικα που έχει ήδη γραφτεί.
Είναι χρήσιμο να διαιρούμε μια μεγάλη αλλαγή σε μικρότερα commits ή να επαναφέρουμε/κάνουμε checkout συγκεκριμένες αλλαγές.

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

## Άλλα ενδιαφέροντα πράγματα

- https://whatthecommit.com/
- https://gitmoji.carloscuesta.me/

## Σας άρεσε;

[Πείτε ευχαριστώ!](https://saythanks.io/to/RomuloOliveira)

## Συνεισφορά

Κάθε είδους βοήθειας θα ήταν καλοδεχούμενη. Παράδειγμα από θέματα με τα οποία μπορείτε να με βοηθήσετε:

- Διορθώσεις στην γραμματική και την ορθογραφία
- Μετάφραση σε άλλες γλώσσες
- Βελτίωση της αναφοράς πηγών
- Λανθασμένη ή ατελής πληροφορία

## Εμπνεύσεις, πηγές, και τι να διαβάσετε περαιτέρω

- [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
- [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Pro Git Book - Rewriting History](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
