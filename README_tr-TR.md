# Commit mesajları kılavuzu

[![Say Thanks!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/RomuloOliveira)

Commit mesajlarının önemini ve onların nasıl yazılacağını anlatan bir rehberdir.

Bu, belki commit'in ne olduğunu öğrenmenize yardımcı olabilir. İyi mesajlar yazmanın neden önemli olduğu, faydalı uygulamalar, iyi bir commit geçmişi planlamak ve (yeniden) yazmak için bazı ipuçları içerir.

## "commit" nedir?

Basitçe, commit yerel deponuza yazılan dosyalarınızın anlık görüntüsüdür.
Bazı insanların düşündüğünün aksine, [git sadece dosyalar arasındaki farkı saklamaz, tüm dosyaların tam sürümünü saklar](https://git-scm.com/book/eo/v1/Ekkomenci-Git-Basics#Snapshots,-Not-Differences).
Bir commit 'ten diğerine değişmemiş dosyalar için, git zaten saklanan önceki özdeş dosyaya yalnızca bir bağlantı oluşturur.

Aşağıdaki resimde git'in her "sürüm"de commit edilidği zaman verilerin nasıl saklandığı gösterilmektedir:

![](https://i.stack.imgur.com/AQ5TG.png)

## Commit mesajları neden önemlidir?

- Kod incelemelerini hızlandırmak ve kolaylaştırmak
- Değişimin anlaşılmasına yardımcı olmak
- Sadece kodla açıklanamayan "neden"leri açıklamak
- Gelecekteki bakımcılara değişikliklerin neden ve nasıl yapıldığını anlamalarına yardımcı olur, sorun giderme ve hata ayıklamayı kolaylaştırır

Bu sonuçları en üst düzeye çıkarmak için, bir sonraki bölümde açıklanan bazı faydalı uygulamaları ve standartları kullanabiliriz.

## Faydalı uygulamalar

Bunlar deneyimlerimden, internet makalelerimden ve diğer kılavuzlardan toplanan bazı uygulamalardır. Başka fikirleriniz varsa (veya bazılarına katılmıyorsanız) bir Pull Request açmaktan ve katkıda bulunmaktan çekinmeyin.

### Zorunluluk biçimini kullanın

```
# Good
Use InventoryBackendPool to retrieve inventory backend
```

```
# Bad
Used InventoryBackendPool to retrieve inventory backend
```

_Ama neden zorunluluk formu?_

Bir commit mesajı başvurulan değişikliğin gerçekte ne yaptığını, etkilerini değil, ne yapıldığını açıklar.

[Chris Beams'in bu muhteşem makalesinde](https://chris.beams.io/posts/git-commit/) bize zorunlu formda daha iyi commit mesajları yazmamamıza yardımcı olmak için kullanılabilecek basit bir cümle veriyor.

```
If applied, this commit will <commit message>
```

Örnekler:

```
# Good
If applied, this commit will use InventoryBackendPool to retrieve inventory backend
```

```
# Bad
If applied, this commit will used InventoryBackendPool to retrieve inventory backend
```

### Büyük harfle başlayın

```
# Good
Add `use` method to Credit model
```

```
# Bad
add `use` method to Credit model
```

İlk harfin büyük harfle yazılmasının nedeni, cümlelerin başında büyük harf kullanma dilbilgisi kuralına uymaktır.

Bu uygulamanın kullanımı kişiden kişiye, takımdan takıma, hatta dilden dile değişebilir. Büyük harfle veya değil, önemli olan nokta tek bir standarda sadık kalmak ve onu takip etmektir.

### Kaynak koda bakmak zorunda kalmadan değişikliğin ne yaptığını bildirmeye çalışın


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

Okuyucuların/Yorumcuların commit edenin ne düşündüğünü anlamalarına yardımcı olmak için birçok senaryoda (_örneğin çoklu commit'ler, çeşitli değişklikler ve yeniden düzenlemeler_) faydalıdır.

### "Neden", "Ne için", "Nasıl"ı ve ek ayrıntıları açıklamak için mesaj gövdesini kullanın

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

Mesajların konusu ve gövdesi boş bir satırla ayrılır.
Ek boş satırlar mesaj gövdesinin bir parçası olarak kabul edilir.

`-`, `*` ve  \` gibi karakterler okunabilirliği artıran öğelerdir.

### Herhangi bir bağlamı olmayan mesajlardan ve genel mesajlardan kaçının

```
# Bad
Fix this

Fix stuff

It should work now

Change stuff

Adjust css
```

### Sütun/karakter sayısını sınırlayın

Konu için en fazla 50 karakter ve gövde için 72 karakter kullanılması [önerilir](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines).

### Dil tutarlılığını koruyun

Proje sahipleri için: bir dil seçin ve tüm commit mesajlarını bu dili kullanarak yazın. İdeal olarak, kod yorumları, varsayılan yerel çeviri ayarları (yerel projeler için) vb. ile eşleşmelidir.

Katkıda bulunanlar için: var olan commit geçmişyle aynı dili kullanarak commit mesajı yazın.

```
# Good
ababab Add `use` method to Credit model
efefef Use InventoryBackendPool to retrieve inventory backend
bebebe Fix method name of InventoryBackend child classes
```

```
# Good (Portekizce örneği)
ababab Adiciona o método `use` ao model Credit
efefef Usa o InventoryBackendPool para recuperar o backend de estoque
bebebe Corrige nome de método na classe InventoryBackend
```

```
# Bad (İngilizce ve Portekizce karışık)
ababab Usa o InventoryBackendPool para recuperar o backend de estoque
efefef Add `use` method to Credit model
cdcdcd Agora vai
```

### Şablon

Bu şablonun orjinali [Tim Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html) tarafından yazıldı; [_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project).

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

## Rebase vs. Birleştirme

Bu kısım **TL;DR** (Too long; didn't read/Çok uzundu; okuyamadım) Atlassian'nın harika eğitimi; ["Birleştirme vs. Rebasing"](https://www.atlassian.com/git/tutorials/merging-vs-rebasing).

![](https://wac-cdn.atlassian.com/dam/jcr:01b0b04e-64f3-4659-af21-c4d86bc7cb0b/01.svg?cdnVersion=hq)

### Rebase

**TL;DR:** Branch commit'inizi tek tek uygulayarak taban dalına uygur ve yeni bir ağaç oluşturur.

![](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=hq)

### Birleştirme

**TL;DR:** Yeni bir commit oluşturup, iki dal arasındaki farklarla (uygun bir şekilde) _merge commit_'i olarak adlandırılır.

![](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=hq)

### Neden bazı kişiler birleştirme (merge) üzerinde rebase tercih eder?

Özellikle birleştirme üzerinde rebase tercih ederim. Sebepleri ise şunlardır:

* Gereksiz bir birleştirme commit'i olmadan "temiz" bir geçmiş oluşturur.
* _Gördüğünüz şey, elde ettiğiniz şeydir_, yani bir kod incelemesinde tüm değişiklikler belirli ve başlıklı bir commit'ten gelir ve birleştirme commit'inde gizlenen değişikliklerden kaçınır.
* Daha fazla birleştirme, commit eden tarafından çözümlenir ve her bir birleştirme değişikliği uygun bir iletiyle bir commit içindedir.
    * Bir birleştirme commit'ini kazmak (_anlamak_) ve gözden geçirmek olağandışı bir durumdur, bu nedenle bunlardan kaçınarak tüm değişikliklerin ait oldukları bir commit'e sahip olmasını sağlar.

### Ne zaman squash (ezme/birleştirme) yapılmalı?

"Squashing" bir dizi commit'i alıp tek bir commit'e yoğunlaştırma işlemidir.

Bazı durumlarda faydalıdır, örneğin:

- Çok az ya dahiç bağlam olmadan commit'i azaltmak (yazım hatası düzeltmeleri, biçimlendirme, unutulmuş şeyler).
- Birlikte uygulandığında daha anlamlı hale gelen ayrı değişikliklere katılma.
- _Devam eden_ commit'leri yeniden yazma

### Rebase veya squash'dan ne zaman kaçınmalıyız?

Genel bir commit'te veya birden fazla kişinin çalıştığı paylaşılan brach/dallarda yeniden oluşturup squash etmekten kaçının. Rebase ve squash yeniden yazma geçmişi ve var olan commit'in üzerine yazmak, paylaşılan branch/dallarda commmit üzerinde değişiklik yapmak karşıklığa (örn., uzaktaki bir depoya push edilen/gönderilen commit veya diğer branch/dallardan gelen commitler) neden olabilir ve insanlar farklı ağaçlar ve çatışmalar nedeniyle değişikliklerini (hem yerel hem de uzaktan) kaybedebilir.

## Kullanışlı git komutları

### rebase -i

Commit squash/sıkıştırmak, mesajları düzenlemek, yeniden yazmak/silmek/düzenlemek vb. İçin kullanın.

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

#### Onarmmak

Commit'i kolayca ve daha karmaşık bir rebase'e gerekmeden temizlemek için kullanın.
[Bu yazıda](http://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html), nasıl ve ne zaman yapılacağına dair güzel örnekler vardır.

### cherry-pick

Yanlış bir branch üzerinde yaptığınız commit'i tekrar kodlamaya gerek kalmadan uygulamak için yararlıdır.

Örnek:

```
$ git cherry-pick 790ab21
[master 094d820] Fix English grammar in Contributing
 Date: Sun Feb 25 23:14:23 2018 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### add/checkout/reset [--patch | -p]

Diyelim ki aşağıdaki gibi bir farkımız var:

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

Zaten yazılmış olan kodu değiştirmeye gerek kalmadan, yalnızca istediğimiz yamaları eklemek için `git add-p`'yi kullanabiliriz.
Büyük bir değişikliği daha küçük bir commit'e bölmek veya belirli değişiklikleri sıfırlamak/kontrol etmek için yararlıdır.

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

## Diğer ilginç şeyler

- https://whatthecommit.com/
- https://gitmoji.carloscuesta.me/

## Beğendin mi?

[Teşekkür Et!](https://saythanks.io/to/RomuloOliveira)

## Katkıda bulunma

Her türlü yardım takdir edilecektir. Bana yardımcı olabileceğiniz örnek konular:

- Dilbilgisi ve yazım düzeltmeleri
- Diğer dillere çeviri
- Kaynak/referans iyileştirme
- Yanlış veya eksik bilgiyi düzeltme

## İlhamlar, kaynaklar ve ileri okuma

- [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
- [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Pro Git Book - Rewriting History](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
