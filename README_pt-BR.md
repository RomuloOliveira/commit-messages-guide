# Guia de mensagens de commit

[![Diga obrigado!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/RomuloOliveira)

Um guia para entender a importância das mensagens de commit e como escrevê-las bem.

Pode te ajudar a aprender o que é um _commit_, entender porque é importante escrever boas mensagens usando boas práticas e conhecer dicas para planejar e (re)escrever o seu histórico de _commits_.

**Observações:** Apesar da versão em português ter sido escrita antes da versão em inglês, a versão inglês contém alguns textos que estão mais detalhados, assim como melhor referenciamento de fontes.

## O que é um "_commit_"?

Em termos simples, o **_commit_** é uma espécie de _snapshot_ dos seus arquivos locais gravado localmente no seu repositório. Ao contrário do que se pensa, o git *não* armazena apenas as diferenças e sim a cópia completa dos arquivos.
No caso de arquivos que não mudaram de um _commit_ para o outro, é gravada uma referência ao arquivo gerado no último snapshot.

A imagem abaixo mostra como o git armazena dados ao longo do tempo com uma versão para cada _commit_:

![](https://i.stack.imgur.com/AQ5TG.png)

## Por que as mensagens são importantes?

- Facilita e agiliza o _code review_
- Ajuda no entendimento do que está acontecendo
- Explica os porquês ocultos que não podem ser explicados somente em código
- Facilita a solução de problemas e a depuração garantindo que futuros codificadores entendam por que e como as mudanças foram feitas

## Boas práticas

### Use o imperativo

```
# Good
Use InventoryBackendPool to retrieve inventory backend
```

```
# Bad
Used InventoryBackendPool to retrieve inventory backend
```

Por que!?

A mensagem de _commit_ diz o que ele **faz**, não o que foi feito.

Regrinha de ouro para mensagens:

```
If applied, this commit will: <commit message>
```

```
# Good
If applied, this commit will: Use InventoryBackendPool to retrieve inventory backend
```

```
# Bad
If applied, this commit will: Used InventoryBackendPool to retrieve inventory backend
```

### Primeira letra em maiúsculo

```
# Good
Add `use` method to Credit model
```

```
# Bad
add `use` method to Credit model
```

É uma regra bem discutível e a menos importante pra mim.
O motivo de escolher começar com letra maiúscula é simplesmente porque é assim
que se começa uma frase em qualquer texto.

### Tente comunicar o que o _commit_ faz sem que seja necessário olhar o conteúdo do _commit_

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

### Use o corpo da mensagem para explicar "porquê", "para quê", "como" e detalhes adicionais

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
Add `use` method to Credit

Change from namedtuple to class because we need to
setup a new attribute (in_use_amount) with a new value
```

O título e o corpo da mensagem são separados por uma linha em branco.
Linhas em branco adicionais são consideradas como parte do corpo.

Caracteres como `-` e `*` e \` são elementos comuns para melhorar a leitura.

### Evite _commits_ com mensagens genéricas ou sem contexto algum

```
# Bad
Fix this

Fix stuff

Agora vai

Change stuff

Adjust css
```

### Tente limitar o nº de colunas das mensagens

[Recomenda-se](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines) 50 caracteres para o título e por volta de 72 para o corpo.

### Mantenha consistência de idioma

```
# Good
ababab Add `use` method to Credit model
efefef Use InventoryBackendPool to retrieve inventory backend
bebebe Fix method name of InventoryBackend child classes
```

```
# Good
ababab Adiciona o método `use` ao model Credit
efefef Usa o InventoryBackendPool para recuperar o backend de estoque
bebebe Corrige nome de método na classe InventoryBackend
```

```
# Bad
ababab Usa o InventoryBackendPool para recuperar o backend de estoque
efefef Add `use` method to Credit model
cdcdcd Agora vai
```

### Exemplo de formato

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

![](https://wac-cdn.atlassian.com/dam/jcr:01b0b04e-64f3-4659-af21-c4d86bc7cb0b/01.svg?cdnVersion=hq)

### Rebase

**TL;DR:** Aplica os _commits_ do seu _branch_, um a um, sobre o _branch_ de base, gerando uma nova árvore

![](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=hq)

### Merge

**TL;DR:** Cria um novo _commit_, chamado de _Merge commit_, com as diferenças entre a sua árvore e a árvore de base

![](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=hq)

### Por que algumas pessoas preferem rebase?

Eu particularmente prefiro o rebase, alguns motivos incluem:

* Deixa o histórico mais "limpo", sem _commits_ de _merge_ desnecessários espalhados nele
* _What you see is what you get_, i.e., em um code review você está vendo o diff real entre o _master_ e o _branch_
* Os conflitos mais complexos são resolvidos pelo _commiter_ e ficam dentro de um _commit_, que tem mensagem e propósito
    * Ninguém olha o conteúdo dos _commits_ de _merge_ e nisso que mora o perigo

### Quando fazer squash

Squash é o processo de pegar uma série de commits e juntá-los em um commit só.

É útil em diversas situações, como por exemplo:

- Muitos _commits_ adicionais sem contexto (correção de _typos_, formatação, coisas esquecidas)
- Mudanças que estão em _commits_ separados que fariam mais sentido parte de um só
- _Commits WIP_

### Quando evitar rebase ou squash?

Evite _rebase_ e _squash_ em _commits_ públicos ou em _branches_ compartilhadas que outras pessoas possam ter trabalhado.
_Rebase_ e _squash_ reescrevem a história sobrescrevendo commits existentes, fazendo isso em commits que existam em _branches_ compartilhadas (i.e., _commits_ enviados para repositórios remotos ou originados de outras branches) podem causar confusão e as pessoas podem perder suas modificações (tanto locais quanto remotas) por causa de divergências e conflitos.

## Comandos úteis

### rebase -i

Usado para fazer _squash_, editar mensagens, editar/apagar/reordenar _commits_, etc.

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

Útil para facilitar a limpeza sem perder tempo/trabalho com um rebase.
[Exemplos](http://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html).

### cherry-pick

Bastante útil quando você precisa pegar aquele _commit_ que você fez no branch errado sem precisar reescrever novamente.

Exemplo:

```
$ git cherry-pick 790ab21
[master 094d820] Fix English grammar in Contributing
 Date: Sun Feb 25 23:14:23 2018 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### add/checkout/reset [--patch | -p]

Exemplo de diff:

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

Podemos usar `git add -p` para adicionar apenas os patches que queremos, sem a necessidade de alterar o código que já está escrito.
É útil para dividir uma grande mudança em commits menores ou para fazer reset/checkout de mudanças específicas.

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

## Links interessantes

- https://whatthecommit.com/
- https://gitmoji.carloscuesta.me/

## Gostou?

[Mandar um obrigado!](https://saythanks.io/to/RomuloOliveira)

## Contribuindo

Todo tipo de ajuda é bem-vinda. Exemplos de tópicos em que você pode contribuir:

- Correcões gramaticais e ortográficas
- Tradução para novas línguas
- Melhoras nas referências e fontes

## Inspirações, fontes e leitura adicional

- [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
- [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Pro Git Book - Rewriting History](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
