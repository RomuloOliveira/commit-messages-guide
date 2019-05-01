# 커밋 메시지 가이드

[![감사 인사하기!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/RomuloOliveira)

커밋 메시지의 중요성을 이해하고 어떻게 하면 잘 작성할 수 있는지에 대해 설명하는 안내서입니다.

커밋 메시지가 무엇이며, 왜 잘 작성하는 것이 중요한지 알아보고 좋은 커밋 히스토리를 유지하고 싶을 때 적용할 수 있는 최고의 접근법과 몇 가지 유용한 팁을 배워봅시다.

## "commit" 이 무엇인가요?

간단히 말해서, "커밋 (commit)" 은 로컬 저장소에 쓰여지는 로컬 파일들의 단편본입니다.
일반적으로 사람들이 생각하는 것과는 다르게, [git은 파일의 변경된 내용만을 기록하지 않고 모든 파일의 버전을 모두 기록합니다](https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-Git-%EA%B8%B0%EC%B4%88#_%EC%B0%A8%EC%9D%B4%EA%B0%80_%EC%95%84%EB%8B%88%EB%9D%BC_%EC%8A%A4%EB%83%85%EC%83%B7).
어떤 한 커밋과 다른 커밋 사이에 변경된 내용이 없다면, git은 이미 동일한 파일에 대해 링크만 생성합니다.

아래의 이미지는 시간이 지남에 따라 git이 어떻게 데이터를 저장하는지 보여줍니다. 각 "Version" 은 커밋을 뜻합니다.

![](https://i.stack.imgur.com/AQ5TG.png)

## 왜 커밋 메시지가 중요한가요?

- 코드 리뷰 시간을 단축하고 능률적으로 처리하기 위해서
- 변경 사항을 이해하는데 도움을 주기 위해서
- 코드만으론 설명이 어려운 "왜 이렇게 했을까" 를 설명하기 위해서
- 추후 작업할 사람이 왜/어떻게 변경 사항이 만들어졌는지 이해하는데 도움을 주고 문제 해결과 디버깅을 쉽게 만들기 위해서

이로부터 얻는 이로운 효과를 극대화 하기 위해, 활용할 수 있는 좋은 습관과 표준을 다음 섹션에서 설명합니다.

## 좋은 습관

다음 설명할 습관들은 제 개인적인 경험, 인터넷 글, 다른 가이드에서 얻어온 것입니다. 더 추가할 내용(또는 뺄 내용)이 있다면 Pull Request 를 열고 기여해주세요.

### 명령조 사용하기

```
# 좋음
InventoryBackendPool을 사용하여 재고 백엔드를 검색합니다
---
Use InventoryBackendPool to retrieve inventory backend
```

```
# 나쁨
InventoryBackendPool을 사용하여 재고 백엔드를 검색했습니다
---
Used InventoryBackendPool to retrieve inventory backend
```

_근데 왜 명령조를 쓰나요?_

커밋 메시지는 무엇이 변경되었는지가 아니라 실제로 그 변경 사항이 미치는 영향, 즉 변경 사항이 실질적으로 무엇을 하는지 설명합니다.

[Chris Beams이 작성한 이 멋진 글](https://chris.beams.io/posts/git-commit/)이 더 나은 커밋 메시지를 명령조로 작성할 때 사용할 수 있는 간단한 문장 하나를 제시합니다:

```
적용 시, 이 커밋은 <커밋 메시지> 합니다
---
If applied, this commit will <commit message>
```

예시:

```
# 좋음
적용 시, InventoryBackendPool을 사용하여 재고 백엔드를 검색합니다
---
If applied, this commit will use InventoryBackendPool to retrieve inventory backend
```

```
# 나쁨
적용 시, InventoryBackendPool을 사용하여 재고 백엔드를 검색했습니다
---
If applied, this commit will used InventoryBackendPool to retrieve inventory backend
```

### 첫 번째 문자를 대문자로 시작하기

```
# 좋음
Add `use` method to Credit model
```

```
# 나쁨
add `use` method to Credit model
```

첫 문자를 대문자로 작성해야 하는 이유는 문장의 시작 부분에 대문자를 사용하는 문법 규칙을 따르기 위함입니다.

이런 실질적인 규칙의 사용상은 사람, 팀, 언어마다 다를 수 있습니다.
대문자로 시작하건 아니건, 중요한 것은 하나의 표준을 만들어 계속 따르는 것입니다.

_역주:_ 한국어는 크게 영향이 없을 듯 합니다.

### 소스코드를 보지 않고도 변경 사항이 무엇을 하는지 알 수 있도록 하기

```
# 좋음
Credit 모델에 `use` 메소드 추가
---
Add `use` method to Credit model
```

```
# 나쁨
`use` 메소드 추가
---
Add `use` method
```

```
# 좋음
텍스트 상자와 레이아웃 프레임 사이 왼쪽 간격 늘림
---
Increase left padding between textbox and layout frame
```

```
# 나쁨
CSS 조정
---
Adjust css
```

이는 다양한 상황 (e.g. 다중 커밋, 서로 다른 변경 사항, 리팩토링)에서 코드 리뷰를 진행하는 사람이 커밋 작성자가 무슨 생각을 하고 있었는지 쉽게 이해할 수 있도록 도움을 줄 수 있습니다.

### 커밋 메시지 본문으로 "왜", "무엇을 위해", "어떻게" 변경했는지와 상세 내용 추가 설명하기

```
# 좋음
InventoryBackend 자식 클래스의 메소드 이름 수정

InventoryBackend를 상속받는 클래스가 기반 클래스의 인터페이스를 따르지 않음.

Cart가 잘못된 방식으로 백엔드 구현을 호출하고 있었기 때문에 문제가 없었음.
---
Fix method name of InventoryBackend child classes

Classes derived from InventoryBackend were not
respecting the base class interface.

It worked because the cart was calling the backend implementation
incorrectly.
```

```
# 좋음
Credits을 cart의 json에 직렬화 및 역직렬화합니다

Credit 객체를 딕셔너리로 전환하는데 두 가지 이유가 있습니다:

  - Pickle이 클래스의 파일 경로에 의존하기 때문에 리팩토링시 로직이 망가질 수 있습니다
  - 딕셔너리와 빌트인 타입은 기본적으로 pickle 모듈에 의해 직렬화가 가능합니다
---
Serialize and deserialize credits to json in Cart

Convert the Credit instances to dict for two main reasons:

  - Pickle relies on file path for classes and we do not want to break up
    everything if a refactor is needed
  - Dict and built-in types are pickleable by default
```

```
# 좋음
Credit에 `use` 메소드 추가

새 속성(in_use_amount)값이 필요하기 때문에 namedtuple에서 클래스로 전환했습니다
---
Add `use` method to Credit

Change from namedtuple to class because we need to
setup a new attribute (in_use_amount) with a new value
```

제목과 메시지 본문은 공백 행 하나로 분리합니다.
이후 추가되는 공백은 메시지 본문의 일부로 취급합니다.

`-`, `*`, \` 와 같은 문자를 사용하면 가독성을 향상시킬 수 있습니다.

### 맥락 없는 총칭적 메시지 사용 자제하기

```
# 나쁨
이거 고침

뭔가 고침

이제 잘 작동할거임

뭔가 변경함

CSS 조정
---
Fix this

Fix stuff

It should work now

Change stuff

Adjust css
```

### 행 글자 수 제한하기

제목은 50자, 본문은 72자로 한 줄에 들어갈 수 있는 글자 수를 제한하는 것이 [권장됩니다](https://git-scm.com/book/ko/v2/%EB%B6%84%EC%82%B0-%ED%99%98%EA%B2%BD%EC%97%90%EC%84%9C%EC%9D%98-Git-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8%EC%97%90-%EA%B8%B0%EC%97%AC%ED%95%98%EA%B8%B0#_commit_guidelines).

### 일정한 언어 사용하기

프로젝트 소유자인 경우: 언어 하나를 선택해서 모든 커밋을 그 언어만 사용해서 작성합니다. 궁극적으로, 이 규칙은 코드 주석과 기본 언어 파일 (다국어 지원 프로젝트의 경우) 등 모두 일치해야 합니다.

기여자의 경우: 이미 커밋 히스토리에서 사용되고 있는 언어를 사용하여 커밋 메시지를 작성합니다.

```
# 좋음
ababab Add `use` method to Credit model
efefef Use InventoryBackendPool to retrieve inventory backend
bebebe Fix method name of InventoryBackend child classes
```

```
# 좋음 (한국어 예시)
ababab Credit 모델에 `use` 메소드 추가
efefef InventoryBackendPool을 사용하여 재고 백엔드를 검색합니다
bebebe InventoryBackend 자식 클래스의 메소드 이름 수정
```

```
# 나쁨 (영어와 한국어 혼용)
ababab Credit 모델에 `use` 메소드 추가
efefef Use InventoryBackendPool to retrieve inventory backend
cdcdcd 이제 잘 작동할거임
```

### 템플릿

이 템플릿은 [_Pro Git Book_](https://git-scm.com/book/ko/v2/%EB%B6%84%EC%82%B0-%ED%99%98%EA%B2%BD%EC%97%90%EC%84%9C%EC%9D%98-Git-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8%EC%97%90-%EA%B8%B0%EC%97%AC%ED%95%98%EA%B8%B0)에 나와있는 [Tim Pope의 커밋 메시지](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)를 발췌한 것입니다.

```
여기에 최대 50자까지 변경 사항에 대해 설명하세요

필요하다면 여기에 좀 더 상세하게 설명하세요. 한 줄당 대략 72자까지 맞출 수 있도록
합니다. 일부 상황에서 첫 줄은 커밋의 제목이 되고, 그 후에 작성되는 텍스트는 본문으로
취급됩니다. 제목과 본문을 나누는 중간에 삽입되는 공백 행은 매우 중요합니다 (본문을
완전히 생략하지 않는 이상); `log` 와 `shortlog`, `rebase` 와 같이 다양한
도구들은 공백에 의존하므로 두 부분을 합쳐버릴 경우 도구가 혼동할 수 있습니다.

이 커밋이 해결하고자하는 문제를 설명합니다. 어떻게 했는지보단(코드가 설명할 것이기 때문),
왜 변경 사항을 적용했는지에 대해 집중합니다. 이 변경 사항으로 인해 생기는 부수 효과가
있거나 다른 직관적이지 않은 영향이 있을 수 있다면 여기에 설명하세요.

앞으로 추가되는 문단은 공백 행 뒤에 옵니다.

 - 필요하다면 강조점을 써도 됩니다

 - 하이픈(-) 또는 별(*)이 주로 강조점으로 사용되고 이후 단일 공백(space)을 삽입합니다
   강조점 사이에는 공백 행을 넣지만 규칙은 언제든지 바꿀 수 있습니다

이슈 트래커를 사용한다면 다음과 같이 레퍼런스를 메시지 하단에 삽입하세요:

이슈: #123
같이보기: #456, #789
---
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

## 재정렬 (Rebase) vs. 병합 (Merge)

이 섹션은 Atlassian의 멋진 튜토리얼 ["Merging vs. Rebasing"](https://www.atlassian.com/git/tutorials/merging-vs-rebasing) 의 **길어서 안 읽음 요약 좀 (TL;DR)** 버전입니다.

![](https://wac-cdn.atlassian.com/dam/jcr:01b0b04e-64f3-4659-af21-c4d86bc7cb0b/01.svg?cdnVersion=hq)

### 재정렬 (Rebase)

**한 줄 요약:** 기반 브랜치부터 작업 브랜치의 커밋을 하나씩 차곡차곡 이어붙여 새로운 트리를 만듭니다.

![](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=hq)

### 병합 (Merge)

**한 줄 요약:** 두 브랜치의 변경 사항을 하나로 합쳐 (적절히) _병합된 커밋_ 이라 적힌 하나의 새 커밋을 만듭니다.

![](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=hq)

### 왜 사람들은 병합(merge)보다 재정렬(rebase)을 선호하나요?

다음과 같은 이유 때문에 저도 병합보단 재정렬을 선호합니다:

- 불필요한 병합된 커밋 없이 "깔끔한" 기록을 생성합니다
- _보이는 그대로 알 수 있습니다_, 특히, 코드 리뷰에서 커밋의 변경 사항을 병합된 커밋으로 인해 감춰지지 않고 모두 볼 수 있습니다
- 커미터(committer)가 더 직접적으로 병합에 관여하게 되고, 모든 병합 변경 사항이 적절한 커밋 메시지로 대체됩니다
  - 병합 커밋을 리뷰하고 파고드는 일은 드묾으로, 병합을 피하면 모든 변경 사항이 각자 적절한 커밋에 연관되도록 할 수 있습니다.

### 스쿼시(squash)가 필요할 때

"스쿼싱 (Squashing)" 은 일련의 커밋을 받아서 하나의 커밋으로 간략화시키는 작업입니다.

다음과 같은 상황에 유용할 수 있습니다:

- 맥락이 없거나 너무 작은 커밋들 줄이기 (오타 교정, 코드 정리, 잊어버린 부분 추가)
- 하나로 합쳤을 때 더 의미가 있는 변경 사항들
- _현재 작업 중 (work in progress)_ 커밋 재작성

### 어떨 때 재정렬(rebase), 스쿼시(squash)의 사용을 피해야 하나요?

재정렬과 스쿼시 모두 공개된 커밋이나 많은 사람들이 같이 작업하는 공유된 브랜치에선 사용하지 않는 것이 좋습니다.
재정렬과 스쿼시는 기존 커밋 기록을 다시 작성해서 덮어씌우기 때문에 위에서 언급한 공유된 브랜치(주로, remote로 푸시 된 커밋 또는 다른 브랜치로부터 받은 커밋)에 적용하게 되면 혼란을 빛게되고 분기 트리와 충돌로 인해 다른 사람들이 작업한 변경 사항을 잃을 수도 있습니다(local과 remote 모두).

## 유용한 git 커맨드

### rebase -i

커밋을 스쿼시가 필요할때, 메시지를 변경하거나, 커밋 재작성/삭제/순서 변경이 필요할 때 사용하세요.

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

복잡한 재정렬을 할 필요 없이 쉽게 커밋을 정리할 때 사용하세요. [이 글](http://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html)에서 언제 어떻게 사용해야 하는지 좋은 예시로 설명하고 있습니다.

### cherry-pick

실수로 엉뚱한 브랜치에 커밋을 했을 때 다시 작업할 필요 없이 해당 커밋을 다른 브랜치에 적용시키고 싶을 때 사용하세요.

사용 예시:

```
$ git cherry-pick 790ab21
[master 094d820] Fix English grammar in Contributing
 Date: Sun Feb 25 23:14:23 2018 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### add/checkout/reset [--patch | -p]

다음과 같은 diff가 있다고 가정해 봅시다:

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

`git add -p` 를 사용하면 코드를 건드리지 않고 원하는 부분만 선택하여 스테이지에 추가할 수 있습니다.
큰 변경 사항을 작은 커밋으로 쪼개거나 특정 변경 사항을 reset/checkout 할 때 유용하게 사용할 수 있습니다.

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

## 다른 흥미로운 것들

- https://whatthecommit.com/
- https://gitmoji.carloscuesta.me/

## 맘에 들어요?

[고마웡!](https://saythanks.io/to/RomuloOliveira)

## 기여하기

형식에 상관없이 도움을 주시면 감사하겠습니다. 다음과 같은 주제가 있습니다:

- 문법 또는 철자 교정
- 다른 언어로 번역
- 출처 참조 개선
- 잘못되었거나 완전하지 않은 정보 개선

## 영감, 출처, 더 읽어보기

- [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
- [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Pro Git Book - Rewriting History](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
