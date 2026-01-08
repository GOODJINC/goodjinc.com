---
title: "Hugo 블로그 만들기 (4): 콘텐츠 작성과 마크다운 숏코드 활용"
slug: "hugo-content-writing"
date: 2026-01-08T20:30:00+09:00
description: "Hugo의 Page Bundle 방식을 이용해 이미지를 효율적으로 관리하고, Blowfish 테마의 강력한 숏코드(Alert, Badge 등)를 활용해 풍성한 글을 작성해 봅니다."
series: ["Hugo 블로그 만들기"]
series_order: 4
categories: ["Writing", "Guide"]
tags: ["Markdown", "Front Matter", "Content"]
draft: false
# Thumbnail : https://pixabay.com/photos/typing-apple-computer-computer-desk-4156011/
---

지난 시간까지 블로그의 뼈대를 세우고 예쁘게 꾸미는 작업을 마쳤습니다. 이제 이 멋진 집에 가구를 채워 넣을 시간입니다. 바로 **콘텐츠 작성**입니다.

Hugo는 마크다운(Markdown) 형식을 기반으로 글을 작성합니다. 네이버 블로그나 티스토리 같은 위지윅 에디터(WYSIWYG)가 없지만 다양한 응용이 가능하고 확장성이 좋다는 장점이 있는 것 같습니다.

오늘은 Hugo 방식의 글쓰기 규칙과, 글을 더 이쁘게 꾸며주는 Blowfish 테마의 **숏코드(Shortcodes)** 기능을 알아보겠습니다.

---

## 1. 새 게시글 생성하기

탐색기에서 파일을 직접 만들어도 되지만, Hugo 명령어를 사용하면 날짜와 기본 형식이 포함된 파일을 자동으로 만들어줍니다.

터미널에서 프로젝트 루트로 이동한 뒤 아래 명령어를 입력해 보세요.

```powershell
# hugo new content posts/[게시글 이름]/index.md
hugo new content posts/hello-world/index.md
```

폴더 안의 index.md 파일을 먼저 읽는 것이 기본 프로세스입니다. `index.md` 파일은 기본 언어로 작성하시고, 다른 언어 게시글을 작성한다면 `index.en.md`와 같이 파일을 생성하여 작성해주시면 됩니다.

```Markdown
.
├── content
│   └── posts
│       └── hello-world
│           ├── index.en.md
│           └── index.md
·
```

물론 폴더 구분 없이 posts 폴더 안에 그냥 `hello-world.md`로 파일을 하나만 만들어도 글은 써집니다.

하지만 나중에 이미지를 넣거나 관리할 때 어려움이 생기기 때문에 게시글마다 폴더를 만들어주는 것이 장기적으로 깔끔하게 관리할 수 있는 방법입니다.

---

## 2. Front Matter 설정

생성된 `index.md` 파일을 열어보면 맨 위에 `--- (또는 +++)`로 감싸진 영역이 있습니다. 이곳을 `Front Matter`라고 부르며, 글의 설정 정보를 담는 곳입니다.

```Markdown
---
title: 'Hello World!'
date: 2026-01-08T20:30:00+09:00
categories: ["Blog"]
tags: ["Hugo", "Content"]
draft: true
---
```

- **title**: 게시글의 제목을 설정합니다.
- **date**: 게시글 작성 일자를 설정합니다. 한국은 UTC 시간보다 9시간 빠르기 때문에 시간 뒤에 `+09:00`을 추가 작성해줍니다.
- **categories/tags**: 글의 분류를 지정합니다. 배열 `["A", "B"]` 형태로 여러 개를 넣을 수 있습니다.
- **draft**: 초안 여부입니다. 글을 다 쓰고 발행할 때 `false`로 바꿔주시면 됩니다.

---

## 3. 본문에 이미지 넣기

저는 게시글 안에 포함되는 이미지는 `img/`라는 폴더를 생성한 뒤 그 폴더 안에 이미지 파일을 복사해 넣습니다.

```Markdown
.
├── content
│   └── posts
│       └── hello-world
│           ├── img
│           │   └── universe.jpg
│           ├── index.en.md
│           └── index.md
·
```

예를 들어 hello-world 게시글 폴더 안에 넣고 싶은 이미지 파일(예: universe.jpg)을 복사해 넣습니다. 그리고 본문에는 다음과 같이 작성하면 됩니다.

**작성 코드 :**

```Markdown
<!-- 이미지 경로 : content/posts/hello-world/img/universe.jpg -->

<!-- 캡션 없이 단순 이미지만 표현
기본형식 : ![이미지 설명](이미지 경로)-->
![우주 사진](img/universe.jpg)

<!-- 캡션을 활용하여 이미지와 이미지 설명 문구도 함께 표현
기본형식 : ![이미지 설명](이미지 경로 "캡션 문구")-->
![우주 사진](img/universe.jpg "Image [by Gerd Altmann](https://pixabay.com/users/geralt-9301/) from [Pixabay](https://pixabay.com/illustrations/universe-sky-stars-space-cosmos-2742113/)")
```

**이미지와 캡션을 함께 표현한 결과 :**

![우주 사진](img/universe.jpg "Image [by Gerd Altmann](https://pixabay.com/users/geralt-9301/) from [Pixabay](https://pixabay.com/illustrations/universe-sky-stars-space-cosmos-2742113/)")

---

## 4. 숏코드 활용하기

마크다운 기본 문법(볼드, 리스트, 링크 등)만으로도 충분히 표현 가능하지만 좀 더 다채롭게 표현하고 싶다면 쇼트코드(Shortcodes)를 활용하면 좋습니다.

[Blowfish Shortcodes 공식 매뉴얼](https://blowfish.page/docs/shortcodes/)에서 더 다양하게 확인하실 수 있습니다.

### ① Alert (경고/알림 박스)

중요한 정보나 팁을 강조할 때 사용합니다.

**작성 코드:**

```Markdown
{{</* alert "twitter" */>}}
**Warning!** This action is destructive!
{{</* /alert */>}}
```

**결과:**

{{< alert "twitter" >}} 이것은 Twitter 스타일의 알림 박스입니다. {{< /alert >}}

**종류**: `warning`(노랑), `neutral`(회색), `info`(파랑) 등 다양한 타입을 지원합니다.

### ② Badge (배지)

텍스트 중간에 작은 태그를 달 수 있습니다.

**작성 코드:**

```Markdown
{{</* badge */>}}New Badge{{</* /badge */>}}
```

**결과:**

{{< badge >}}New Badge{{< /badge >}}

### ③ YouTube 영상 삽입

유튜브 영상 ID만 알면 손쉽게 영상을 넣을 수 있습니다.

**작성 코드:**

```Markdown
{{</* youtubeLite id="pNi9PjmbUrI" label="한로로(HANRORO)_입춘(Let Me Love My Youth)" */>}}
```

{{< youtubeLite id="pNi9PjmbUrI" label="한로로(HANRORO)_입춘(Let Me Love My Youth)" >}}

### ④ 코드 블록 (Syntax Highlighting)

개발 블로그의 핵심이죠. 언어를 지정하면 하이라이팅이 적용됩니다. 제가 가장 많이 사용하는 숏코드입니다.

**작성 코드:**

````Plaintext
```python
def hello():
  print("Hello Hugo!")
```
````

**결과:**

```python
def hello():
  print("Hello Hugo!")
```

---

## 5. 실시간 미리보기

글을 쓰거나 블로그 관련 수정 작업 도중에도 터미널에서 `hugo server`를 켜둔 상태라면, 파일을 수정 및 저장(`Ctrl + S`)할 때마다 자동으로 새로고침되어 결과물을 바로 확인할 수 있습니다.

{{< alert >}}
**주의1:** `hugo server`를 실행했는데 글이 안 보인다면 Front Matter의 `draft` 값이 `true`로 되어 있을 가능성이 높습니다. 초안인 상태로 게시글을 보고 싶다면 터미널에서 `hugo server -D` 명령어를 아용해 서버를 실행하면 됩니다.
혹은 `draft` 값을 `false`로 바꾼다면 즉시 확인하실 수 있습니다.
{{< /alert >}}

</br>

{{< alert icon="fire" cardColor="#db2f3dff" iconColor="#ffffff" textColor="#ffffff" >}}
**주의2:** 게시글 작성시간이 빌드날짜보다 미래 시간으로 설정되어 있다면 게시글이 안 보일 수 있습니다. 빌드날짜보다 과거의 시간으로 설정하거나, `config\_default\hugo.toml` 파일에서 `buildFuture`를 설정해주시면 됩니다.
{{< /alert >}}

---

## 6. 마치며

이제 글 쓰는 법과 꾸미는 법을 어느정도 익혔습니다. 로컬(`localhost:1313`)에서 그럴듯하게 블로그가 완성된 것을 확인하셨을겁니다.

블로그를 내가 원하는대로 좀 더 꾸미는 방법은 앞으로도 꾸준히 소개해드리겠습니다.

우선 다음 시간에는 지금까지 만든 나만의 블로그를 **다른 사람들이 접속해서 볼 수 있도록 배포하는 방법**에 대해 소개하겠습니다.
