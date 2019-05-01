# Guía de mensajes de commit

[![Say Thanks!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/RomuloOliveira)

Una guía para entender la importancia de los mensajes de commit y cómo escribirlos correctamente.

Aquí vas a aprender qué es un commit, por qué es importente escribir buenos mensajes, buenas prácticas y algunos tips para planear y (re)escribir una buena historia de commits.

## ¿Qué es un "commit"?

En una frase, un commit es una copia instantánea de los archivos escritos de tu repositorio local.
En contra de lo que mucha gente cree, [git no guarda solo la diferencia entre los archivos, sino que guarda cada versión completa](https://git-scm.com/book/es/v2/Inicio---Sobre-el-Control-de-Versiones-Fundamentos-de-Git#_copias_instant%C3%A1neas_no_diferencias)
Para los archivos que no cambian de un commit a otro, git guarda un enlace a la versión previa, idéntica al archivo guardado.

La imagen a continuación muestra como git guarda datos a través del tiempo, entendiendo que cada "versión" es un commit:

![](https://i.stack.imgur.com/AQ5TG.png)

## ¿Por qué los mensajes de commit son importantes?

- Para acelerar y dinamizar las revisiones de código
- Para ayudar a entender los cambios
- Para explicar los "por qué" que no pueden ser descritos solo con código
- Para ayudar a los mantenedores futuros a entender por qué o cómo se hizo un cambio, facilitando la resolución de problemas y la depuración

Para maximizar estos resultados se pueden usar las buenas prácticas y estándares descritos en la sección siguiente.

## Buenas prácticas

Estas son algunas prácticas recolectadas desde mi experiencia, artículos de internet y otras guías. Si tienes otras (o estás en contra de alguna) siéntete libre de abrir un Pull Request y contribuir.

### Usa forma imperativa

```
# Good
Use InventoryBackendPool to retrieve inventory backend
```

```
# Bad
Used InventoryBackendPool to retrieve inventory backend
```

_¿Pero por qué usar forma imperativa?_

Un mensaje de commit describe qué **hace** el cambio referenciado, su efecto, no qué se hizo.

[Este excelente artículo de Chris Beans](https://chris.beams.io/posts/git-commit/) nos da deja una idea que podemos usar como ayuda para escribir mensajes de commit en forma imperativa:

```
If applied, this commit will <commit message>
```

Ejemplo:

```
# Good
If applied, this commit will use InventoryBackendPool to retrieve inventory backend
```

```
# Bad
If applied, this commit will used InventoryBackendPool to retrieve inventory backend
```

### Primera letra en mayúscula

```
# Good
Add `use` method to Credit model
```

```
# Bad
add `use` method to Credit model
```

El motivo detrás de esto es para seguir la regla gramatical que las oraciones deben comenzar en mayúsculas.

El uso de esta práctica puede variar de persona a persona, de equipo a equipo, o incluso de idioma a idioma.
Mayúsculas o no, es importante adherir a un solo estándar y respetarlo.

### Comunica qué hace el cambio sin necesidad de mirar al código fuente

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

Es muy útil para ayudar a los revisores a entender el razonamiento del autor de los cambios (por ejemplo, cuando hay muchos commits, muchos cambios y refactors)

### Usa el cuerpo del mensaje para explicar "por qué", "para qué", "cómo" y detalles adicionales

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

El asunto y el cuerpo del mensaje se separan por una línea en blanco.
Las líneas en blanco adicionales pasan a ser consideradas parte del cuerpo del mensaje.

Caracteres como `-`, `*` y \` pueden aportar legibilidad.

### Evita mensajes genéricos o sin contexto

```
# Bad
Fix this

Fix stuff

It should work now

Change stuff

Adjust css
```

### Limita el número de columnas

[Se recomienda](https://git-scm.com/book/es/v2/Git-en-entornos-distribuidos-Contribuyendo-a-un-Proyecto#r_commit_guidelines) usar un máximo de 50 caracteres para el asunto y 72 para el cuerpo.

### Mantén idioma consistente

Para dueños de proyectos: elijan un idioma y escriban todos los mensajes de commit usando ese idioma. Idealmente debería coincidir con los comentarios del código, la localización por defecto (para proyectos que apliquen), etc.

Para contribuidores: escriban sus mensajes de commits usando el mismo idioma que los que ya existen en el historial de commits.

```
# Good
ababab Add `use` method to Credit model
efefef Use InventoryBackendPool to retrieve inventory backend
bebebe Fix method name of InventoryBackend child classes
```

```
# Good (Spanish example)
ababab Agrega el método `use` a la clase Credit
efefef Usa el InventoryBackendPool para recuperar el backend de stock
bebebe Corrige el nombre de un método de la clase InventoryBackend
```

```
# Bad (mixes English and Spanish)
ababab Use InventoryBackendPool to retrieve inventory backend
efefef Add `use` method to Credit model
cdcdcd Listo
```

### Plantilla

Esta es una plantilla, [escrita originalmente por Tim Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), que aparece en el [_Libro Pro Git_](https://git-scm.com/book/es/v2/Git-en-entornos-distribuidos-Contribuyendo-a-un-Proyecto).

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

Esta sección es un **TL;DR** del excelente tutorial de Atlassian, ["Merging vs. Rebasing"](https://www.atlassian.com/git/tutorials/merging-vs-rebasing).

![](https://wac-cdn.atlassian.com/dam/jcr:01b0b04e-64f3-4659-af21-c4d86bc7cb0b/01.svg?cdnVersion=hq)

### Rebase

**TL;DR:** aplica los commits de tu rama, uno a uno, sobre la rama base, generando un nuevo árbol.

![](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=hq)

### Merge

**TL;DR:** crea un nuevo commit, llamado (adecuadamente) un _commit de merge_, con la diferencia entre las dos ramas.

![](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=hq)

### ¿Por qué algunas personas prefieren rebase en lugar de merge?

Yo particularmente prefiero rebase por sobre merge. Entre otros, los motivos son:

* Genera una historia más "limpia", sin commits de merge innecesarios
* _Lo que ves es lo que hay_, por ejemplo, en una revisión de código los cambios vendrán de commits específicos y rotulados, evitando cambios ocultos en commits de merge
* Más merges son resueltos por el autor y cada cambio producto de un merge es un commit separado con un mensaje acorde.
    * No es una práctica usual indagar y revisar un commit de merge, así que al evitarlos nos aseguramos que los cambios provengan de un commit particular

### ¿Cuándo hacer squash?

"Squashing" es el proceso de tomar una serie de commits y condensarlos en uno solo.

Es útil en varias situaciones, por ejemplo:

- Reducir commits muy pequeños o sin contexto (typos, formateos, olvidos)
- Unir cambios separados que cobran más sentido cuando se aplican juntos
- Reescribir commits de trabajo en progreso (WIP)

### ¿Cuándo evitar el rebase o squash?

Evita el uso de rebase y squash en commits que sean públicos o compartidos por varias personas que trabajan en simultáneo.
Rebase y squash reescriben la historia y sobreescriben commits existentes, al hacerlo en commits que pertenecen a ramas compartidas (por ejemplo que fueron publicados en un repositorio remoto) puede causar confusión y pérdida del trabajo de alguien (tanto de manera local como remota) por encontrarnos frente a árboles divergentes y conflictos.

## Comandos git útiles

### rebase -i

Úsalo para hacer squash de commits, editar mensajes, reescribir/eliminar/reordenar commits, etc.

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

Úsalo para limpiar commits fácilmente y sin necesidad de un rebase más complejo.
[Este artículo](http://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html) tiene muy buenos ejemplos de cómo y cuándo usarlo.

### cherry-pick

Es útil para aplicar un commit que se hizo en una rama equivocada, sin necesidad de volver a escribirlo.

Ejemplo:

```
$ git cherry-pick 790ab21
[master 094d820] Fix English grammar in Contributing
 Date: Sun Feb 25 23:14:23 2018 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### add/checkout/reset [--patch | -p]

Supongamos que tenemos la siguiente diferencia:

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

Podemos usar `git add -p` para agregar solo los parches que querramos, sin necesidad de cambiar el código que ya fue escrito.
Es útil también para separar un cambio grande en commits pequeños o hacer reset/checkout de cambios específicos.

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

## Otros enlaces interesantes

- https://whatthecommit.com/
- https://gitmoji.carloscuesta.me/

## ¿Te gustó?

[¡Di gracias!](https://saythanks.io/to/RomuloOliveira)

## Contribuciones

Toda ayuda es bienvenida. Ejemplo de temas sobre los que puedes colaborar:

- Correcciones de gramática y ortografía
- Traducción a otros idiomas
- Mejoras en el código de referencia
- Información incorrecta o incompleta

## Fuentes de inspiración, referencias y lecturas adicionales

- [Cómo escribir un mensaje de commit de git](https://chris.beams.io/posts/git-commit/)
- [Libro Pro Git - Guía de commits](https://git-scm.com/book/es/v2/Git-en-entornos-distribuidos-Contribuyendo-a-un-Proyecto#r_commit_guidelines)
- [Una nota sobre mensajes de commit de git](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Libro Pro Git - Reescribiendo la Historia](https://git-scm.com/book/es/v2/Herramientas-de-Git-Reescribiendo-la-Historia)
