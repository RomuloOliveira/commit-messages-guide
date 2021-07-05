# Przewodnik po commitach

[![Podziękuj twórcy!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/RomuloOliveira)

Przewodnik ten, pomoże Ci zrozumieć jak ważne są wiadomości zawierane w commitach i jak je dobrze pisać.

Dodatkowo pomoże Ci zrozumieć czym są same commity, jak ważne jest pisanie dobrych wiadomości, jakie są najlepsze praktyki i wskazówki, do pisania (i poprawienia) naprawdę dobrej historii commitów.

Na potrzeby przewodnika, będziemy używać słowa "commit" - zamiast polskich odpowiedników "popełnić, angażować, oddać, zatwierdzić"
A na wiadomości do commitów (strasznie to brzmi po Polsku) będziemy pisać "commit message"

## Dostępne języki

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
- [ελληνικά](README_gr-GR.md)
- [Française](README_fr-FR.md)
- [پارسی](README_fa-IR.md)
- [Polish](README_pl-PL.md)

## Co to jest "commit"?

W krótkich słowach, commit to _snapshot_ _(migawka)_ Twoich lokalnych plików, zapisana w Twoim lokalnym repozytorium. Czyli ich dokładna kopia.
W przeciwieństwie do tego, co myślą niektórzy, [git nie przechowuje tylko i wyłącznie róznic między plikami, przechowuje pełną warsj wszystkich plików](https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F#_snapshots_not_differences).
Jeżeli któryś plik nie zmienił się między commitami, to git "linkuje" go, po to, by oszczędzić miejsce.

Obrazek poniżej, pokazuje jak git przechowuje dane, każda wersja, to commit:

![](https://i.stack.imgur.com/AQ5TG.png)

## Dlaczego commit messages są ważne?

- Aby przyspieszyć i usprawnić code-reviews (analize i ocenianie kodu przez innych programistów)
- Aby pomóc w zrozumieniu zmiany danego commita
- Aby wyjaśnić „dlaczego” zrobiliśmy coś, ponieważ nie zawsze da się to opisać kodem
- Aby pomóc przyszłym programistom dowiedzieć się, dlaczego i jak dokonano zmian, ułatwiając rozwiązywanie problemów i debugowanie.

Aby zmaksymalizować te punkty, możemy skorzystać z dobrych praktyk i standardów opisanych w następnym rozdziale.

## Dobre praktyki

Oto niektóre praktyki zebrane z moich doświadczeń, artykułów internetowych i innych przewodników. Jeśli masz inne (lub nie zgadzasz się z niektórymi), możesz otworzyć Pull Request i wnieść swój wkład.

Jako że commit messages, piszemy w języku angielskim, nie będą one tłumaczone.

### Użyj trybu rozkazującego

```
# Dobrze
Use InventoryBackendPool to retrieve inventory backend
```

```
# Żle
Used InventoryBackendPool to retrieve inventory backend
```

_Ale po co używać trybu rozkazującego?_

commit message opisuje co zmiana aktualnie **robi**. Chodzi o zmiany w kodzie, a nie o to co zostało zrobione.

[Ten artykuł od Chrisa Beams](https://chris.beams.io/posts/git-commit/) zawiera proste zdanie, które może nam pomóc w pisaniu lepszych komunikatów w trybie rozkazującym:

```
If applied, this commit will <commit message>
```

Examples:

```
# Dobrze
If applied, this commit will use InventoryBackendPool to retrieve inventory backend
```

```
# Żle
If applied, this commit will used InventoryBackendPool to retrieve inventory backend
```

### Zacznij z dużej litery

```
# Dobrze
Add `use` method to Credit model
```

```
# Żle
add `use` method to Credit model
```

Powodem, dla którego pierwsza litera powinna być wielka, jest przestrzeganie prostej zasady gramatycznej, polegającej na używaniu wielkich liter na początku zdania.

Stosowanie tej praktyki może różnić się w zależności od zespołu.

### Staraj się komunikować, co robi zmiana, bez konieczności patrzenia na kod źródłowy

```
# Dobrze
Add `use` method to Credit model

```

```
# Żle
Add `use` method
```

```
# Dobrze
Increase left padding between textbox and layout frame
```

```
# Żle
Adjust css
```

Pomoże Ci to w wielu przypadkach (np. wyszukiwanie danej zmiany w kilku commitach). Nie ma nic gorszego, niż szukanie odpowiedniego commita, wsród kilkunastu z opisem "visual fixes".

### Użyj ciała wiadomości, aby wyjaśnić „dlaczego”, „po co” i „jak”

```
# GoodDobrze
Fix method name of InventoryBackend child classes

Classes derived from InventoryBackend were not
respecting the base class interface.

It worked because the cart was calling the backend implementation
incorrectly.
```

```
# Dobrze
Serialize and deserialize credits to json in Cart

Convert the Credit instances to dict for two main reasons:

  - Pickle relies on file path for classes and we do not want to break up
    everything if a refactor is needed
  - Dict and built-in types are pickleable by default
```

```
# Dobrze
Add `use` method to Credit

Change from namedtuple to class because we need to
setup a new attribute (in_use_amount) with a new value
```

Głowa i ciało wiadomości są oddzielone pustą linią.

Znaki takie jak `-`, `*` i \` znacznie zwiększają czytelność.

### Unikaj ogólnych wiadomości lub wiadomości bez kontekstu

```
# Źle
Fix this

Fix stuff

It should work now

Change stuff

Adjust css
```

### Ogranicz liczbę znaków

[Zalecane jest](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines) używać tylko 50 znaków w temacie (głowie) i 72 w ciele.

### Zachowaj spójność językową

Do właścicieli projektów: wybierz język i pisz wszystkie commit messages w tym języku. Najlepiej by był to ten sam język, w którym znajdują się nazwy zmiennych, metod czy obiektów.
(Najczęściej jest to angielski, chyba że przyjdzie Wam pracować dla PKP)

Dla współtwórców: Pisz commit messages, używając tego samego języka, którego używali poprzedni commitujący.

```
# Dobrze
ababab Add `use` method to Credit model
efefef Use InventoryBackendPool to retrieve inventory backend
bebebe Fix method name of InventoryBackend child classes
```

```
# Dobrze (Portuguese example)
ababab Adiciona o método `use` ao model Credit
efefef Usa o InventoryBackendPool para recuperar o backend de estoque
bebebe Corrige nome de método na classe InventoryBackend
```

```
# Źle (mixes English and Portuguese)
ababab Usa o InventoryBackendPool para recuperar o backend de estoque
efefef Add `use` method to Credit model
cdcdcd Agora vai
```

### Szablon

Oto cytat, [napisany przez Tima Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), Ktory pojawia się w [_Wspaniałej książce o gicie_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project).

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

PL:

```
Podsumuj zmiany w około 50 znakach lub mniej

W razie potrzeby bardziej szczegółowy tekst objaśniający zmieść w 72 znakach.
W niektórych commitach pierwsza linia jest traktowana jako
temat commitu, a reszta tekstu jako jego treść.
pusta linia oddzielająca głowę od ciała jest bardzo ważna (chyba żecałkowicie pomijasz ciało);

Wyjaśnij problem, który rozwiązuje commit. Skoncentruj się na tym, dlaczego
wprowadzasz tę zmianę, a nie na tym jak (kod to wyjaśni).
Czy są jakieś błędy i problemy które tworzy ten commit?
W ciele commitu możesz je wyjaśnić.

Kolejne akapity pojawiają się po pustych wierszach.

 - punktory też są w porządku

 - Zazwyczaj przed punktorem stosuje się myślnik lub gwiazdkę, poprzedzone spacją.

Jeśli korzystasz z narzędzia do śledzenia zgłoszeń, umieść odniesienia do nich na dole,
Na przykład:

Rozwiązuje: #123
Zobacz też: #456, #789
```

## Rebase vs. Merge (Zmiana bazy vs scalanie)

Ta sekcja to **TL;DR** (za długie do czytania) z wspaniałego samouczka Atlassian, ["Merging vs. Rebasing"](https://www.atlassian.com/git/tutorials/merging-vs-rebasing).

![](https://wac-cdn.atlassian.com/dam/jcr:01b0b04e-64f3-4659-af21-c4d86bc7cb0b/01.svg?cdnVersion=hq)

### Rebase (Zmiana bazy)

**TL;DR:** Układa Twoje gałęzie (branch) commitów, jeden po drugim, na gałęzi bazowej, generując nowe drzewo.

![](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=hq)

### Merge (Scalanie)

**TL;DR:** Tworzy nowy commit, nazwany (odpowiednio) _merge commit_, z informacjami o róznicach między gałęziami.

![](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=hq)

### Dlaczego niektórzy wolą zmienić bazę, zamiast scalić?

Ja wolę zmianę bazy. Powodami są:

- Generowanie „czystej” historii, bez zbędnych commitów scalających.
- _What you see is what you get_, (otrzymujesz to co widzisz), to znaczy wszystkie zmiany pochodzą z konkretnych i nazwanych commitów, unikamy zmian wprowadznych w merge commitach.
- Każdy commit jest z odpowiednią wiadomością, a my nie musimy potem kopać w zmianach, które wystąpiły przy scalaniu.

### Kiedu squashować

"Squashing" to proces zbierania serii commitów i kondensowaniu ich w jednym commicie. Czyli polega na "zgnieceniu" kilku commitów w jeden.

Przydaje się to w kilku sytuacjach, np.:

- Redukcja commitów z małą ilością zmian (formatowanie, literówki)
- Łączenie commitów, wprowadzających zmiany, które mają sens tylko jeżeli są razem.
- Nadpisywaniu niedokonczonych commitów.

### Kiedy unikać zmiany bazy lub squasha?

Unikaj zmiany bazy i squasha w publicznych zatwierdzeniach lub w gałęziach współdzielonych, nad którymi pracuje wiele osób.
Zmiana bazy i squash nadpisuję historię i istniejące commity, robienie tego na commitach, które znajdują się we współdzielonych gałęziach (tj. zatwierdzeń wypchniętych do zdalnego repozytorium lub pochodzących z innych gałęzi) może powodować zamieszanie i ludzie mogą utracić swoje zmiany (zarówno lokalnie, jak i zdalnie) z powodu rozbieżnych drzew i konfliktów.

## Przydatne komendy git

### rebase -i

Użyj go do squashowania commitów, edytowania wiadomości, przepisywania/usuwania/zmieniania kolejności zatwierdzeń itp.

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

Użyj go do łatwego czyszczenia commitówm bez potrzeby bardziej złożonej zmiany bazy.
[Ten artykuł](http://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html) zawiera bardzo dobre przykłady, jak i kiedy to zrobić.

### cherry-pick

Bardzo przydatne jest zastosowanie tego commita, który wykonałeś w złej gałęzi, bez konieczności ponownego kodowania.

Przykładowo:

```
$ git cherry-pick 790ab21
[master 094d820] Fix English grammar in Contributing
 Date: Sun Feb 25 23:14:23 2018 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### add/checkout/reset [--patch | -p]

Powiedzmy, że mamy następującą różnicę:

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

Możemy użyć `git add -p` aby dodawać tylko te poprawki, które chcemy, bez konieczności zmiany kodu, który jest już napisany.
Przydatne jest podzielenie dużej zmiany na mniejsze commity, lub zresetowanie/pobranie określonych zmian.

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

## Więcej interesujących linków

- https://whatthecommit.com/
- https://gitmoji.carloscuesta.me/

## Spodobało Ci się?

[Say thanks!](https://saythanks.io/to/RomuloOliveira)

## Contributing

Wszelka pomoc jest mile widziana. Przykładowe tematy, w których możesz mi pomóc:

- Poprawki gramatyczne i ortograficzne
- Tłumaczenie na inne języki
- Poprawa odwoływania się do źródła
- Nieprawidłowe lub niepełne informacje

## Inspiracje, źródła i dalsze lektury

- [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
- [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Pro Git Book - Rewriting History](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
