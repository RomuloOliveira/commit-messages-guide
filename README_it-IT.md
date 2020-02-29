# Guida per i messaggi di commit

[![Ringrazia!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/RomuloOliveira)

Una guida per capire l'importanza dei messaggi di commit e come scriverli bene.

Potrebbe aiutarti a capire cos'è un commit, perché è importante scrivere buoni messaggi, buone pratiche e alcuni consigli per pianificare e (ri)scrivere una buona storia per i commit.

## Cos'è un "commit"?

In termini semplici, un commit è una _fotografia_ dei file locali, scritti nel repository locale.
Contrariamente a cosa pensano alcune persone, [git non memorizza solo le differenze tra i file, ma la versione completa di tutti i file](https://git-scm.com/book/eo/v1/Ekkomenci-Git-Basics#Snapshots,-Not-Differences).
Per i file che non cambiano tra un commit e l'altro, git memorizza solo un link al file identico precedente che è già memorizzato.

L'immagine qui sotto mostra come git memorizza i dati nel tempo, nella quale ogni "Version" è un commit:

![](https://i.stack.imgur.com/AQ5TG.png)

## Perché i messaggi di commit sono importanti??

- Per velocizzare e snellire la _code review_ (revisione del codice)
- Per aiutare la comprensione di un cambiamento
- Per spiegare i motivi del cambiamento, che non possono essere spiegati con il solo codice
- Per aiutare i _maintainers_ futuri a capire perché e come i cambiamenti sono stati fatti, rendendo la futura individuazione e risoluzione di problemi più facile

Per massimizzare questi risultati, possiamo usare alcune buone pratiche e standard descritti nella prossima sezione.

## Buone pratiche

Queste sono alcune (buone) pratiche collezionate dalla mia esperienza, da articoli su internet, e altre guide. Se ne avete altre (o non siete d'accordo su alcune) sentitevi liberi di aprire una Pull Request e contribuire.

### Uso della forma imperativa

```
# Corretto
Usa InventoryBackendPool per recuperare il backend dell'inventario
```

```
# Errato
Usato InventoryBackendPool per recuperare il backend dell'inventario
```

_Ma perché usare la forma imperativa?_

Un messaggio di commit descrive cosa fa il cambiamento (a cui fa riferimento), i suoi effetti,, non cosa è stato fatto.

[Questo ottimo articolo di Chris Beams](https://chris.beams.io/posts/git-commit/) fornisce una semplice frase che può essere usata per aiutarci a scrivere messaggi di commit in modo imperativo in modo Inglese. Riadattato alla sintassi Italiana:

```
Questo commit <messaggio di commit in forma presente>
```

oppure

```
Se applicato, questo commit <messaggio di commit in forma presente>
```

Esempi:

```
# Corretto
Se applicato, questo commit usa InventoryBackendPool per recuperare il backend dell'inventario
```

```
# Errato
Se applicato, questo commit usato InventoryBackendPool per recuperare il backend dell'inventario
```

### La prima lettera in maiuscolo

```
# Corretto
Aggiunge il metodo `use` al modello Credit
```

```
# Errato
aggiunge il metodo `use` al modello Credit
```

Il motivo per mettere la prima lettera iniziale è per seguire le regole grammaticali che impongono la lettera maiuscola ad inizio di una frase.

L'uso di questa pratica può variare da persona a persona, gruppo a gruppo, o anche da lingua a lingua. In maiuscolo o no, l'importante è usare un solo standard e seguirlo.

### Tenta di comunicare cosa il cambiamento fa senza la necessità di guardare il codice

```
# Corretto
Aggiunge il metodo `use` al modello Credit

```

```
# Errato
Aggiunge il metodo `use`
```

```
# Corretto
Incrementa il padding sinistro tra il textbox e
layout frame
```

```
# Errato
Sistema il CSS
```

E' utile in tanti scenari (esempio: commit multipli, parecchi cambiamenti e ristrutturazioni) per aiutare i revisori a capire cosa il _committer_ (ovvero chi ha fatto il commit) stava pensando.

### Usa il corpo del messaggio per spiegare "perché", "per cosa", "come" e dettagli aggiuntivi

```
# Corretto
Corregge il nome del metodo delle classi figlie
di InventoryBackend

Classi derivate da InventoryBackend non rispettavano la classe base.

Funzionava perché il carrello chiamava l'implementazione di backend non
corretta.
```

```
# Corretto
Serializza e deserializza i crediti in JSON in
Cart

Converte le istanze di Credit in dizionario per due motivi:

  - Pickle si basa sul percorso del file per le classi e non vogliamo
    rompere tutto se ci sarà una ristrutturazione
  - Dizionari e tipi built-in sono pickleable by default
```

```
# Corretto
Aggiunge il metodo `use` a Credit

Cambia da namedtuple a classe perché abbiamo bisogno di preparare un
nuovo attributo (in_use_amount) con un nuovo valore
```

L'oggetto ed il corpo del commit sono separati da una linea vuota.
Linee vuote aggiuntive sono considerate parte del messaggio.

Caratteri come `-`, `*` e \` sono elementi che aiutano la leggibilità.

### Evita messaggi di errore generici o messaggi senza contesto

```
# Errati
Correggi questo

Corrette delle cose

Ora dovrebbe funzionare

Cambia delle cose

Aggiusta il css
```

### Limita il numero di colonne

[E' consigliato](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines) usare al massimo 50 caratteri per l'oggetto e 72 per il corpo di ogni commit.

### Mantieni la lingua in modo consistente

Per i proprietari dei progetti: scegli una lingua e scrivi tutti i messaggi di commit in quella lingua. Sarebbe l'ideale se fosse la stessa lingua con cui si scrivono i commenti nel codice, la stessa predefinita per l'applicazione, ecc.

Per chi collabora: scrivi i messaggi dei tuoi commit rispettando la stessa lingua della history dei commit.

```
# Corretto
ababab Aggiunge il metodo `use` al modello Credit
efefef Usa InventoryBackendPool per recuperare il backend dell'inventario
bebebe Correggi il nome del metodo delle classi figlio di InventoryBackend
```

```
# Corretto (esempio in Portuguese)
ababab Adiciona o método `use` ao model Credit
efefef Usa o InventoryBackendPool para recuperar o backend de estoque
bebebe Corrige nome de método na classe InventoryBackend
```

```
# Errato (mischia English e Portuguese)
ababab Usa o InventoryBackendPool para recuperar o backend de estoque
efefef Add `use` method to Credit model
cdcdcd Agora vai
```

### Modelli

Questo è un modello, [scritto originariamente da Tim Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), che appare in [_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project).

```
Raccogli i cambiamenti in 50 caratteri o meno

Una spiegazione più dettagliata se necessario. Vai a capo a circa 72
caratteri. In alcuni contesti, la prima linea è trattata come oggetto
del commit, ed il resto come il corpo. La linea vuota che separa
l'oggetto dal corpo è necessaria (amenoché il corpo non sia vuoto);
vari strumenti come `log`, `shortlog` e `rebase` possono confondersi se
li metti insieme.

Spiega il problema che questo commit risolve. Focalizzati sul perché
stai facendo questo cambiamento al contrario di come (il codice lo
spiega già di suo). Ci sono side-effects o altre conseguenze non
intuitive a seguito di questo cambiamento? Questo è il posto per
spiegarle.

Altri paragrafi vengono dopo linee vuote.

 - Elenchi puntati vanno bene

 - Di solito un trattino o un asterisco son usati per il punto,
   preceduti da un singolo spazio, con linee vuote nel mezzo, ma qui le
   convenzioni variano

Se hai un sistema di tracciamento delle issues, puoi mettere i
riferimenti alla fine, così:

Risolve: #123
Vedi anche: #456, #789
```

## Rebase vs. Merge

Questa sezione è un **TL;DR** degli eccellenti tutorial di Atlassian, ["Merging vs. Rebasing"](https://www.atlassian.com/git/tutorials/merging-vs-rebasing).

![](https://wac-cdn.atlassian.com/dam/jcr:01b0b04e-64f3-4659-af21-c4d86bc7cb0b/01.svg?cdnVersion=hq)

### Rebase

**TL;DR:** Applica i commit del tuo branch, uno a uno, al branch di base, generato un nuovo albero.

![](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=hq)

### Merge

**TL;DR:** Crea un nuovo commit, chiamato (propriamente) _merge commit_, con le differenze tra i due branches.

![](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=hq)

### Perché qualcuno preferisce "rebase" a "merge"?

Anche io, tra i tanti, preferisco "rebase" a "merge". Le motivazioni sono, tra le altre:

* Genera una history "pulita", senza _merge commits_ non necessari
* _What you see is what you get_, ovvero in una revisione del codice tutti i cambiamenti arrivano da uno specifico commit, evitando cambiamenti nascosti nei _merge commits_
* Più merges sono risolti da chi crea il commit, e ogni cambiamento in un merge è un commit con un proprio messaggio
    * E' poco comune guardare e revisionare i commit di merge, quindi evitarli del tutto assicura che tutti i cambiamenti sono sotto il commit dove dovrebbero essere

### Quando fare lo "squash"

"Squashing" (o _fare squash_) è il processo di prendere diversi commit e condensarli all'interno di un singolo unico commmit.

E' utile quando, ad esempio, si vuole:

- Ridurre i commit con poco o nulla (correzioni di errori ortografici o simili, formattazione, cose dimenticate)
- Unire cambiamenti sperati che hanno più senso applicati insieme
- Riscrivere un commit che era _work in progress_

### Quando evitare "rebase" o "squash"?

Evita "rebase" e "squash" in commit pubblici, oppure in branch condivisi dove più persone stanno lavorando.
"Rebase" e "squash" riscrivono la storia e sovrascrivono i commit esistenti: fare questo in commit che sono in branch condivisi (ovvero, sincronizzati con repository remoti) può causare confusione, e le persone potrebbero perdere il proprio lavoro (locale o remoto) a causa di alberature divergenti e conflitti.

## Comandi git utili

### rebase -i

Usa per fare uno "squash", modificare messaggi, riscrivere/eliminare/riordinare i commit, etc.

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

Usa per pulire i commit in modo semplice e senza un rebase "complesso".
[Questo articolo](http://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html) ha dei buoni esempi su come e quando fare ciò.

### cherry-pick

E' utile per applicare un commit fatto in un altro branch (anche per errore), senza aver bisogno di riscriverlo.

Esempio:

```
$ git cherry-pick 790ab21
[master 094d820] Fix English grammar in Contributing
 Date: Sun Feb 25 23:14:23 2018 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### add/checkout/reset [--patch | -p]

Facciamo il caso di avere il seguente _diff_:

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

Possiamo usare `git add -p` per aggiungere solo le patch che vogliamo, senza aver bisogno di cambiare il codice che è già scritto.
E' utile per spezzare grandi cambiamenti in piccoli commit, o per fare il reset/checkout di cambiamenti specifici.

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

## Altre cose interessanti

- https://whatthecommit.com/
- https://gitmoji.carloscuesta.me/

## Ti piace?

[Ringrazia!](https://saythanks.io/to/RomuloOliveira)

## Contribuire

Qualsiasi tipo di aiuto è apprezzato. Un esempio di cose per cui potete aiutarmi sono:

- Correzioni grammaticali e ortografiche
- Traduzione in altre lingue
- Miglioramento nei riferimenti alle sorgenti
- Informazioni parziali o incomplete

## Fonti d'ispirazione, sorgenti e altre letture

- [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
- [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Pro Git Book - Rewriting History](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
