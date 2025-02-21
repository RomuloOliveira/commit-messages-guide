# Commit mesajları təlimatı

[![Say Thanks!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/RomuloOliveira)

Bu təlimat commit mesajlarının əhəmiyyətini və onların daha yaxşı necə yazılacağını izah edir.

Bu, "commit"-in nə olduğunu, yaxşı commit mesajları yazmağın nə üçün vacib olduğunu, yaxşı commit tarixçəsini planlaşdırmaq və (yenidən) yazmaq üçün bəzi nümunələr və məsləhətləri anlamağa kömək edə bilər.

## "commit" nədir?

Sadə dillə desək, commit sizin yerli reponuza yazılmış fayllarınızın *anlıq* görüntüsüdür.
Bəzi insanların düşündüyündən fərqli olaraq, [git yalnız fayllar arasındakı fərqləri saxlamır, bütün faylların tam versiyasını saxlayır](https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F#_snapshots_not_differences).
İki commit arasında dəyişməmiş fayllar üçün git, sadəcə olaraq, artıq saxlanmış əvvəlki eyni fayla keçid yaradacaq.

Aşağıdakı şəkil, git-in hər bir "versiya"ya uyğun olaraq məlumatları necə saxladığını göstərir:

![](https://i.stack.imgur.com/AQ5TG.png)

## Commit mesajları niyə vacibdir?

- Kod baxışını (code review) daha sürətli və asan edir
- Dəyişikliyi anlamağa kömək edir
- Təkcə kodla izah edilə bilməyən "niyə"ni izah edir
- Sonrakı tərtibatçılara dəyişikliklərin niyə və necə edildiyini anlamağa kömək edir, problemlərin aradan qaldırılmasını və xətaların düzəldilməsini asanlaşdırır.

Bu faydaları maksimum dərəcədə artırmaq üçün biz növbəti bölmədə təsvir olunan bəzi ən yaxşı təcrübə və standartlardan istifadə edə bilərik.
## Ən yaxşı təcrübələr

Bunlar təcrübələrimdən, internetdəki məqalələrdən və digər təlimatlardan topladığım bəzi təcrübələrdir. Əlavə etmək istədiyiniz bir şey varsa (və ya razı deyilsinizsə), Pull Request açın və töhfə verin.

### Əmr formasından istifadə edin

```
# Good
Use InventoryBackendPool to retrieve inventory backend
```

```
# Bad
Used InventoryBackendPool to retrieve inventory backend
```

_Bəs nə üçün əmr forması?_

Commit mesajı göstərilən dəyişiklikdə nə edildiyini deyil, əslində, nə etdiyini və onun təsirlərini təsvir edir.

### Böyük hərf ilə başlayın

```
# Good
Add `use` method to Credit model
```

```
# Bad
add `use` method to Credit model
```

Böyük hərflə başlamağın səbəbi, qrammatik qaydalardan biri olan cümlələrin əvvəlində böyük hərflərdən istifadəyə riayət etməkdir.

Bunun istifadəsi insandan insana, komandadan komandaya və hətta dildən dilə dəyişə bilər. Böyük hərflə yazın və ya yazmayın, əsas məsələ bir standarta bağlı qalmaq və ona əməl etməkdir.

### Mənbə koduna baxmadan dəyişikliyin nə etdiyini bildirməyə çalışın

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

Bu təcrübə bir çox ssenarilərdə (məsələn, çoxlu commitlər, çoxsaylı dəyişikliklər və refaktorinqlər zamanı) mesaj oxuyanlara xəbər verənin nə düşündüyünü anlamağa kömək etmək üçün faydalıdır.

### "Niyə?", "Nə məqsədlə?", "Necə?" suallarını və əlavə detalları izah etmək üçün mesaj mətnindən istifadə edin

“Nə” əvəzinə “niyə”yə diqqət yetirin (baxmayaraq ki, “nə” və “necə” hələ də vacibdir).
Məsələn, commit mesajınız diff-in yenidən ifadəsidirsə, onu yenidən nəzərdən keçirmək vacib ola bilər.

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

Mesajların mövzusu və mətni boş sətirlə ayrılır.
Əlavə boş sətirlər mesajın əsas hissəsi hesab olunur.

`-`, `*` və \` kimi simvollar oxunaqlılığı artıran elementlərdir.

###  Ümumi və ya hərhansı konteksti olmayan mesajlardan çəkinin

```
# Bad
Fix this

Fix stuff

It should work now

Change stuff

Adjust css
```


### "this PR", "this commit", "this patch" kimi yazı dilindən çəkinin

Bir commitin özünə müraciət etmək lazım deyil. Biz **bilirik** ki, bu, yol, commit və ya PR-dır.

```
# Bad
This commit does x and y...

This PR does x and y...

This Patch x and y...

# Good

X and y are done...
```

### Şəxsi dildən çəkinin (məsələn, əvəzliklər)

Akademik yazılardan öyrənib, mesajların göndərilməsinə də tətbiq edə biləcəyimiz bir şey, şəxsi dildən istifadə etməməkdir.

```
# Bad
I fixed the problem.

# Good
The problem has been fixed by doing x and y...
```

### Simvolların sayını məhdudlaşdırın

Mövzu üçün 50 simvoldan, mətn üçün isə 72 simvoldan çox olmamaq [tövsiyə olunur](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines).
### Dil ardıcıllığını qoruyun

Layihə sahibləri üçün: Bir dil seçin və bütün commit mesajlarını həmin dildə yazın. İdeal olaraq, kod şərhləri, standart yerli tərcümə parametrləri (lokallaşdırılmış layihələr üçün) və s. ilə uyğun gəlməlidir.

Töhfə verənlər üçün: Mövcud commit tarixçəsi ilə eyni dildən istifadə edərək commit mesajı yazın.

```
# Good
ababab Add `use` method to Credit model
efefef Use InventoryBackendPool to retrieve inventory backend
bebebe Fix method name of InventoryBackend child classes
```

```
# Good (Portuqalca nümunə)
ababab Adiciona o método `use` ao model Credit
efefef Usa o InventoryBackendPool para recuperar o backend de estoque
bebebe Corrige nome de método na classe InventoryBackend
```

```
# Bad (İngiliscə və Portuqalca qarışıq)
ababab Usa o InventoryBackendPool para recuperar o backend de estoque
efefef Add `use` method to Credit model
cdcdcd Agora vai
```

### Şablon

Bu şablonun orijinalı [Tim Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html) tərəfindən yazılıb: [_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project).

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


## PR mesajları və müşayiət məktubları haqqında qeydlər

Əksər tərtibatçılar Git reposunda Pull Request (PR) yaratmaq üçün bir platformadan (GitHub, GitLab) istifadə edirlər, lakin nüvə (kernel) tərtibatçıları və dəyişiklikləri e-poçt vasitəsilə göndərən şəxslər ([bəli, belə bir şey var](https://git-scm.com/docs/git-send-email/2.45.0) ) bunu "cover letter" (müşayiət məktubu) adlandırırlar.

Yaxşı bir müşayiət məktubu və ya PR mesajı bir-biri ilə əlaqəli olan commit seriyasını ümumiləşdirir, onların mənşəyi və konteksti haqqında məlumat verir. Bu hissənin yaxşı yazılması commit seriyanızı layihənin saxlayıcılarına "satmağa" kömək edəcək, çünki onlar təqdim etdiyiniz dəyişikliklərin niyə birlikdə göndərildiyini asanlıqla anlaya biləcəklər.

Əgər daha kiçik (bir və ya bir neçə commit-lik) dəyişiklik edirsinizsə, ilk commit-i müşayiət məktubu kimi qəbul edin. Məsələn, GitHub ilk commit-i standart PR mesajı kimi istifadə edir.

Linux nüvəsi (kernel) e-poçt siyahısına göndərilmiş yaxşı bir müşayiət məktubunun [nümunəsi budur](https://lore.kernel.org/lkml/20230414225551.858160935@linutronix.de/). O, aşağıdakıları ehtiva edir:

- Ümumi dəyişikliklərin təsviri və onların hansı səbəblə edildiyi;
- Bu dəyişiklikləri anlamaq üçün vacib olan arxa plan və digər mühüm məlumatlar;
- Həllin detallı izahı və bu həllə çatmaq üçün tətbiq edilən yanaşma;
- Çətinliklər və ya tətbiq etməzdən əvvəl nəzərə alınmalı potensial problemlər;
- Mümkün təkmilləşdirmələr – cari commit dəstinin əhatə dairəsindən kənarda qalan gələcək dəyişikliklər üçün imkanları təsvir edən bölmə.

## Commit-ləri imzalamaq və qaydalara riayət etmək

Açıq mənbə (open-source) layihələr tez-tez kodunuzu imzalamağı və müəyyən qaydalara əməl etməyi tələb edir. Bunun bir nümunəsi **Developer Certificate of Origin (DCO)**-dur ([DCO saytı](https://developercertificate.org/)), hansı ki, **The Linux Foundation**, **Cloud Native Computing Foundation** və digər təşkilatların layihələrinə töhfə verərkən riayət etməli olduğunuz bir qaydadır.

Bu o deməkdir ki, siz **həqiqi adınızdan** istifadə etməlisiniz (yəni, sizi müəyyən edən bir ad, _mütləq hüquqi adınız olmalı deyil_) və commit-lərinizi imzalamalısınız. Təxəllüslərdən və ya saxta adlardan istifadə etməyin. **Həqiqi adlardan istifadə haqqında daha ətraflı** [buradan oxuya bilərsiniz](https://www.mail-archive.com/kernelnewbies@kernelnewbies.org/msg22178.html).

Adınızı və e-poçtunuzu təyin etmək üçün aşağıdakı `git config` əmrlərindən istifadə edin:

``` sh
# Bu dəyişiklikləri yerli olaraq tək repoya tətbiq edə bilərsiniz
git config --local user.name "Jane Doe"
git config --local user.email "janedoe@janedoe.com"

# Və ya qlobal olaraq
git config --global user.name "Jane Doe"
git config --global user.email "janedoe@janedoe.com"
```

Commit edərkən `git commit` əmrinə `-s` bayrağını əlavə edin. Bu, commit-inizə **"Signed-off-by: "** sətrini əlavə edəcək.

Bu sətrin commit-ə əlavə olunmasından başqa, commit-lərinizi imzalamaq üçün **GPG (GNU Privacy Guard)** istifadə etmək də vacibdir.

GPG (və ya GNU Privacy Guard) sənədləri şifrələməyə və onların dəyişdirilməsinin qarşısını almağa imkan verən bir alətdir. Məsələn, e-poçtları imzalamaq və onların sizin razılığınız olmadan dəyişdirilmədiyini təmin etmək üçün istifadə edilə bilər. **Git dünyasında isə GPG commit-in həqiqətən sizin tərəfinizdən edildiyini və başqaları tərəfindən dəyişdirilmədiyini təsdiqləmək üçün istifadə olunur.**

GitHub-da **GPG açarını yaratmaq və hesabınıza əlavə etmək** haqqında daha ətraflı [məlumat](https://docs.github.com/en/authentication/managing-commit-signature-verification/adding-a-gpg-key-to-your-github-account) əldə edə bilərsiniz. **Commit-lər üçün gpgsign istifadəsi** ilə bağlı təlimatı [buradan](https://docs.github.com/en/authentication/managing-commit-signature-verification/telling-git-about-your-signing-key) oxuya bilərsiniz.

**GPG ilə işləmək haqqında daha çox məlumatı** [buradan](https://git-scm.com/book/en/v2/Git-Tools-Signing-Your-Work) əldə edə bilərsiniz.

Daha yüksək təhlükəsizlik üçün [pinentry](https://www.gnupg.org/related_software/pinentry/index.html) konfiqurasiya edə bilərsiniz. Bu, GPG üçün fiziki təhlükəsizlik qatlarını əlavə etməyə, məsələn, commit-lərinizi **Yubikey və ya Touch ID** ilə imzalamağa imkan verir.

## Rebase (yenidən baza) və Merge (birləşmə)

Bu hissə, Atlassian-ın ["Merging vs. Rebasing"](https://www.atlassian.com/git/tutorials/merging-vs-rebasing) adlı möhtəşəm dərsliyinin TL;DR (Too long; didn't read/çox uzun idi; oxumadım) xülasəsidir.
![](https://wac-cdn.atlassian.com/dam/jcr:01b0b04e-64f3-4659-af21-c4d86bc7cb0b/01.svg?cdnVersion=hq)

### Rebase

**TL;DR:** Bu, branch commitlərini əsas branch-dan sonra yeni ağac yaratmaq üçün bir-bir tətbiq edir.

![](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=hq)

### Merge

**TL;DR:** İki branch arasındakı fərqləri ehtiva edən _merge commit_ adlı yeni commit yaradır.

![](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=hq)

### Niyə bəzi insanlar merge (birləşmə) əvəzinə rebase-ə (yenidən baza) üstünlük verirlər?

Şəxsən mən merge yerinə rebase-ə üstünlük verirəm. Səbəblər aşağıdakılardır:

* Gereksiz bir _merge commit_'i olmadan "temiz" bir geçmiş oluşturur.
* _Gördüğünüz şey, elde ettiğiniz şeydir_, yani bir kod incelemesinde, merge commit'inin ardında gizlenen değişikliklerden kaçınarak, tüm değişiklikler belirli ve başlıklı bir commit'ten gelir.
* Daha fazla merge, commit eden tarafından çözümlenir ve her bir merge işlemi uygun bir mesajla bir commit içindedir.
    * Bir birleştirme commit'ini detaylı incelemek ve gözden geçirmek olağandışı bir durumdur, bu nedenle bunlardan kaçınmak tüm değişikliklerin ait oldukları bir commit'e sahip olmasını garanti eder.

- Lazımsız bir _merge commit_'i olmadan "təmiz" bir tarix yaradır.
- _Gördüyün şey, əldə etdiyin şeydir_, yəni kod icmalında merge commit-inin arxasında gizlənmiş dəyişikliklərdən qaçaraq, bütün dəyişikliklər müəyyən və başlıqlı bir commit-dən gəlir.
- Daha çox merge commit edən tərəfindən həll edilir və hər bir merge əməliyyatı uyğun bir mesajla commit içərisində olur.
    - Bir merge commit-inin detallı incələnməsi və nəzərdən keçirilməsi qeyri-adi bir vəziyyətdir, buna görə də bunlardan qaçmaq bütün dəyişikliklərin aid olduqları bir commit-ə sahib olmasını təmin edir.

### Squash (əzmə/birləşdirmə) nə zaman edilməlidir?

"Squashing" bir sıra commit-i götürüb tək bir commit-ə sıxlaşdırmaq prosesidir.

Bəzi hallarda faydalıdır, məsələn:
- Çox az və ya heç bir konteksti olmayan commit-ləri azaltmaq (orfoqrafiya səhvlərinin düzəldilməsi, formatlama, unudulmuş şeylər)
- Birlikdə tətbiq edildikdə daha məntiqli olan ayrıca dəyişiklikləri birləşdirmək
- Üzərində işlənməyə davam edilən commit-ləri yenidən yazmaq

### Rebase və ya squash-dən nə zaman çəkinməlisiniz?

_Public commit_-lərdə və ya bir neçə nəfərin birlikdə işlədiyi paylaşılan branch-lərdə rebase və squash-dən çəkinin. Rebase və squash tarixçəni yenidən yazır və mövcud commit-lərin üzərinə yazır. Bunu paylaşılan branch-lərdə etmək qarışıqlığa səbəb ola bilər (məsələn, uzaq repo-ya push edilən commit-lər və ya digər branch-lərdən gələn commit-lər). Bu, insanların fərqli branch-lər və konfliktlər səbəbindən dəyişikliklərini (həm yerli, həm də uzaq) itirməsinə səbəb ola bilər.

## Faydalı git əmrləri

### rebase -i

Commitləri squash/sıxışdırmaq, mesajları redaktə etmək, commitləri yenidən yazmaq/silmək/sıralarını düzəltmək vs s. üçün istifadə olunur.

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

Commitləri asanlıqla və daha mürəkkəb bir rebase-ə ehtiyac olmadan təmizləmək üçün istifadə olunur.
[Bu yazıda](http://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html), necə və nə vaxt ediləcəyinə dair gözəl nümunələr var.

### cherry-pick

Səhv branch-da etdiyiniz commiti yenidən kodlaşdırma etmədən tətbiq etmək lazım olduqda bu çox faydalıdır.

Nümunə:

```
$ git cherry-pick 790ab21
[master 094d820] Fix English grammar in Contributing
 Date: Sun Feb 25 23:14:23 2018 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### add/checkout/reset [--patch | -p]

Deyək ki, aşağıdakı kimi bir _diff_'imiz var:

```diff
diff --git a/README.md b/README.md
index 7b45277..6b1993c 100644
--- a/README.md
+++ b/README.md
@@ -186,10 +186,13 @@ bebebe Corrige nome de método na classe InventoryBackend
 ``
 # Bad (mixes English and Portuguese)
 ababab Usa o InventoryBackendPool para recuperar o backend de estoque
-efefef Credit modeline `use` metodu ekle
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

Artıq yazılmış kodu dəyişdirmədən yalnız istədiyimiz yolları əlavə etmək üçün `git add-p` istifadə edə bilərik.
Böyük dəyişikliyi daha kiçik commitlərə bölmək və ya xüsusi dəyişiklikləri sıfırlamaq/kontrol etmək üçün faydalıdır.

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
-efefef Credit modeline `use` metodu ekle
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

## Digər maraqlı şeylər

- https://whatthecommit.com/
- https://gitmoji.carloscuesta.me/

## Bəyəndin?

[Təşəkkür et!](https://saythanks.io/to/RomuloOliveira)

## Töhfə vermək

Hər hansı bir yardım təqdirəlayiqdir. Mənə kömək edə biləcəyiniz mövzuların nümunələri:

- Qrammatika və orfoqrafiya düzəlişləri
- Digər dillərə tərcümə
- Mənbə/istinadın təkmilləşdirilməsi
- Yanlış və ya natamam məlumatların düzəldilməsi

## İlham alınanlar, mənbələr və əlavə oxu

- [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
- [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Pro Git Book - Rewriting History](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
