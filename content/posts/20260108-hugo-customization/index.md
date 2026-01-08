---
title: "Hugo 블로그 만들기 (3): 언어 설정 및 메뉴 커스터마이징"
slug: hugo-customization
date: 2026-01-08T08:40:00+09:00
description: "Blowfish 테마의 설정 파일 구조를 이해하고, 블로그 언어를 한국어로 변경하며 프로필과 메뉴를 구성하는 방법을 다룹니다."
series: ["Hugo 블로그 만들기"]
series_order: 3
categories: ["Hugo", "Customization"]
tags: ["TOML", "Configuration", "Menu", "Profile", "i18n"]
draft: false
# Thumbnail : https://pixabay.com/photos/code-programming-coding-web-2434271/
---

지난 2편에서 Blowfish 테마를 적용하고 서버를 띄우는 것까지 성공했습니다. 하지만 화면에 보이는 건 기본 세팅된 간단한 화면 뿐이었죠.

이번 시간에는 블로그를 내가 원하는대로 커스터마이징하는 방법을 소개합니다. 저도 아직 하나씩 적용해보고 테스트해보는 입장이지만 기본적인 설정 방법에 대해 소개합니다.

---

## 1. 설정 파일의 구조 이해하기

일반적인 Hugo 테마는 `hugo.toml` 파일 하나에 대부분의 설정을 작성합니다. 하지만 Blowfish는 설정 관리를 편하게 하기 위해 파일을 쪼개서 관리합니다.

`config/_default/` 폴더를 열어보면 다음과 같은 파일들이 보일 것입니다.

- **hugo.toml**: 사이트의 가장 기본 정보 (URL, 타이틀, 테마 지정)
- **languages.toml**: 언어 설정 (한국어, 영어 등)
- **menus.toml**: 상단 메뉴(Header)와 하단 메뉴(Footer) 설정
- **params.toml**: 디자인, 프로필, 기능 켜기/끄기 등 **일반적인 테마에 대한 설정**

저희는 이 4가지 파일을 조금씩 수정해보겠습니다.

---

## 2. 한국어로 설정하기

가장 먼저 블로그의 기본 언어를 한국어로 바꿔보겠습니다.

### ① hugo.toml 수정

`defaultContentLanguage` 값을 `en`에서 `ko`로 변경합니다.

```toml
# config/_default/hugo.toml
theme = "blowfish"
baseURL = "https://goodjinc.com"
defaultContentLanguage = "ko"
```

### ② languages.toml 수정

Blowfish는 다국어를 지원하기 때문에 언어별 설정이 따로 필요합니다. 기존에 있던 `languages.toml` 파일 이름을 `languages.ko.toml`로 수정한 뒤 문서를 수정해줍니다.

저는 한글과 영어를 모두 지원할 예정이기 때문에 총 2개의 파일(`languages.ko.toml`과 `languages.en.toml`)을 생성합니다.

언어 코드에 대한 자세한 설명은 [BlowFish 공식 매뉴얼](https://blowfish.page/docs/configuration/#language-and-i18n)에서도 확인 가능합니다.

```TOML
# config/_default/languages.ko.toml

languageCode = "ko"
languageName = "Korean"
weight = 10
title = "GOODJINC"

[params]
  displayName = "Korean"
  isoCode = "ko"
```

```TOML
# config/_default/languages.en.toml

languageCode = "en"
languageName = "EN"
weight = 20
title = "GOODJINC"

[params]
  displayName = "English"
  isoCode = "en"
```

`displayName`을 통해서 아래와 같이 리스트에서 표현되는 명칭을 설정할 수 있으며, `weight` 값을 통해서 순서를 설정해줄 수 있습니다.

{{< figure src="img/languages-setting-result.png" alt="Languages Setting Result" >}}

---

## 3. 프로필 및 디자인 설정

블로그 메인 화면에 들어갔을 때 가장 먼저 보이는 프로필 사진과 소개 글을 수정해 봅시다. 이 설정은 `params.toml`에서 담당합니다.

### ① 디자인 테마

Blowfish는 blowfish, congo, github 등 다양한 색상 테마를 제공합니다. `params.toml` 파일에서 설정할 수 있습니다.

[BlowFish 공식 매뉴얼](https://blowfish.page/docs/getting-started/#colour-schemes)에도 미리 체험해본 뒤 마음에 드는 테마를 고르시면 됩니다.

```TOML
# config/_default/params.toml

colorScheme = "github"
```

### ② 홈페이지 설정

`params.toml` 파일의 `[homepage]` 섹션을 찾아 아래와 같이 수정합니다.

```TOML
# config/_default/params.toml

[homepage]
  layout = "profile" # 배경 이미지가 있는 hero 스타일 또는 심플한 profile 스타일 중 추천
  showRecent = true # true로 설정 시 최근 게시글이 함께 보임
```

저는 작가의 프로필과 최신 글이 가장 먼저 보이도록 위와 같이 설정했습니다.

### ③ 프로필 설정

작가의 프로필 이미지가 설정되어 있지 않기 때문에 의도한대로 표현이 안될 수 있습니다.

작가의 프로필 이미지는 `assets/img/` 폴더를 만든 뒤 해당 폴더 안에 `author.jpg`라는 이름의 이미지 파일을 추가하도록 합니다.

이후 `languages.ko.toml` 파일에서 아래와 같이 작가 정보를 설정합니다.

`languages.en.toml` 파일을 수정하여 영어일 때의 작가 정보를 다르게 설정하는 것도 가능합니다.

```TOML
[params.author]
  name = "GOODJINC" # 작가명
  email = "hello@goodjinc.com" # 작가 이메일
  image = "img/author.jpg" # 작가 프로필 이미지
  headline = "1%의 당신으로부터" # Homepage에서 표현되는 문장
  bio = "1%의 당신으로부터" # 게시글 내 작가의 한마디에 표현되는 문장
  links = [
    { email = "mailto:hello@goodjinc.com" },
    { github = "https://github.com/goodjinc" },
  ]
```

이 곳에서 설정한 작가 프로필은 홈페이지 뿐 아니라 게시글 내부의 작가 프로필 등 다양한 곳에서 활용되기 때문에 고민하여 작성 합니다.

{{< figure src="img/author-profile-setting-result-ko.png" alt="Author Profile Setting Result" >}}

---

## 4. 메뉴 구성하기

메뉴바 헤더(Header)에 메뉴를 추가해 보겠습니다. `menus.ko.toml` 파일에서 아래와 같이 편집합니다.

영어 버전일 때의 메뉴는 `menus.en.toml`에서 설정하여 한글과 영어일 때의 메뉴 구성을 다르게 하는 것도 가능합니다.

```TOML
# config/_default/menus.ko.toml

[[main]]
  name = "About"
  pageRef = "about" # content/about/index.md 파일을 만들어줘야 함
  weight = 10

[[main]]
  name = "Posts"
  pageRef = "posts" # content/posts 폴더와 연결
  weight = 20

[[main]]
  name = "Series"
  pageRef = "series"
  weight = 30
```

- **weight**: 숫자가 작을수록 왼쪽에 배치됩니다.
- **pageRef**: 연결할 콘텐츠의 경로입니다.

웹사이트 하단에 메뉴를 추가하고 싶은 경우 `menus.ko.toml` 파일에 아래 코드도 추가해줍니다.

```TOML
# config/_default/menus.ko.toml

 [[footer]]
   name = "Tags"
   pageRef = "tags"
   weight = 10

 [[footer]]
   name = "Categories"
   pageRef = "categories"
   weight = 20
```

---

## 5. 결과 확인

모든 수정을 마쳤다면 터미널에서 `hugo server`를 작성하여 실행해봅니다.

이미 서버가 가동중이었다면 자동으로 갱신되어 표현이 될텐데, 혹시나 무슨 문제가 발생하여 ERROR가 발생했다면 다시 시작해주세요.

웹사이트 메인 페이지에 수정된 부분이 잘 반영되었는지 확인해봅니다.

아직 게시글을 작성하지 않았기 때문에 글이 보이거나 메뉴 이동에 제한이 있을 수 있습니다.

---

## 6. 마치며

이제 블로그의 외형적인 부분은 어느정도 완성되었습니다. 다음 편에서는 이제 가장 중요한 **콘텐츠**를 작성해보도록 하겠습니다.
