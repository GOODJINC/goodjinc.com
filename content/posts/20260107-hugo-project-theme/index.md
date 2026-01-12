---
title: "Hugo 블로그 만들기 (2): 프로젝트 생성 및 Blowfish 테마 적용"
slug: hugo-project-theme
date: 2026-01-07T12:20:00+09:00
description: "Hugo로 새로운 블로그 프로젝트를 생성하고, Git Submodule을 이용해 Blowfish 테마를 설치하는 방법을 단계별로 알아봅니다."
series: ["Hugo 블로그 만들기"]
series_order: 2
categories: ["Hugo", "Web Development", "Tutorial"]
tags: ["Hugo", "SSG", "Blog", "Blowfish", "Theme", "Git", "Submodule", "Config"]
showTableOfContents: true
draft: false
# Thumbnail : https://unsplash.com/photos/person-typing-on-laptop-computer-3GZNPBLImWc
---

지난 1편에서 윈도우 환경에 Hugo(Extended 버전) 설치까지 완료했습니다. 이제 본격적으로 나만의 블로그를 만들고, **Blowfish**테마를 적용해보도록 하겠습니다.

---

## 1. 새 Hugo 프로젝트 생성

원하는 폴더(예: `C:\Project`)로 이동한 뒤, 터미널에서 아래 명령어를 입력하여 새로운 사이트를 생성합니다. 블로그 이름을 `my-blog`로 정했습니다.

```Powershell
hugo new site my-blog
```

명령어가 성공하면 `my-blog`라는 폴더가 생깁니다. 이제 해당 폴더로 들어갑니다.

```PowerShell
cd my-blog
```

{{< figure src="img/hugo-new-site.png" alt="Command Result: Hugo New Site" >}}

**주요 파일 및 폴더 파악**

- hugo.toml: 블로그의 설정을 담당하는 가장 중요한 파일
- content 폴더: 내가 작성할 글(Markdown)이 저장되는 곳
- themes 폴더: 다운로드한 테마가 저장되는 곳
- static 폴더: 이미지, robots.txt 등 정적 파일 보관소
- layouts 폴더: 테마를 내 입맛대로 수정할 때 쓰는 오버라이드 폴더

---

## 2. Git 초기화 (Git Init)

Hugo는 Git 사용을 적극 권장하고 있습니다. 그리고 대부분의 테마들이 Git을 통해 배포하고 있기 때문에 Git을 사용해줍니다.

우선은 프로젝트 폴더 루트에서 Git을 초기화해 줍니다.

```PowerShell
git init
```

이 단계가 선행되어야 나중에 테마를 Submodule 방식으로 관리할 수 있습니다.

---

## 3. Blowfish 테마 설치하기

Hugo에는 수많은 테마가 있지만, 저는 Blowfish를 선택했습니다. 아직은 기술적인 부분들보다는 디자인과 문서화된 설명들이 많은지만 봤습니다.

그리고 npm 등 기타 기술들이 추가적으로 들어간 테마가 있었는데, 해당 부분은 아직 잘 모르기 때문에 제외했습니다.

Hugo 테마를 한눈에 볼 수 있는 [공식 테마 사이트](https://themes.gohugo.io/)가 있으니 이 곳에서 마음에 드는 테마를 찾으시면 됩니다.

테마를 설치하는 방법이 여러가지가 있지만, 유지보수가 가장 편리한 Git Submodule 방식을 사용했습니다.

크게 3가지가 있지만, 유지보수가 가장 편한 Git Submodule 방식을 추천합니다.

```PowerShell
# themes 폴더 안에 blowfish를 서브모듈로 추가
git submodule add -b main https://github.com/nunocoracao/blowfish.git themes/blowfish
```

{{< figure src="img/git-theme-submodule.png" alt="Command Result: git submodule" >}}

{{< alert type="info" >}} 테마 파일을 직접 복사해 넣을수도 있지만, 나중에 테마 개발자가 버그를 수정하거나 새 기능을 추가했을 때 업데이트하기가 매우 번거롭습니다. Submodule을 쓰면 명령어 한 줄로 테마를 최신 상태로 유지할 수 있기 때문에 Submodule 방식을 선택했습니다. {{< /alert >}}

---

## 4. 기본 설정

여기서부터 헷갈리기 시작합니다. Hugo 기본 세팅에서 `hugo.toml` 파일이 루트 폴더에 위치해있습니다.

Blowfish 테마는 루트 폴더에 있는 `hugo.toml`을 삭제하고 `config/_default/` 폴더에서 관리하라고 안내하고 있습니다.

그래서 Blowfish 테마에서 기본 제공하는 `hugo.toml`과 기본 세팅 파일들을 우선 가져오도록 하겠습니다.

더 상세한 내용은 [Blowfish 설치 매뉴얼](https://blowfish.page/docs/installation/#install-using-git)을 참고할 수 있습니다.

① `themes\blowfish\config\_default` 폴더에 있는 모든 파일들을 복사한다.

{{< figure src="img/copy-blowfish-files.png" alt="Copy Blowfish Theme Files" >}}

② 루트 폴더에서 `config\_default` 폴더를 생성한 뒤 해당 폴더 안에 복사한 파일을 붙여넣기한다.

{{< figure src="img/paste-blowfish-files.png" alt="Paste Blowfish Theme Files" >}}

③ `config\_default` 폴더에 있는 `hugo.toml` 파일을 VS Code로 실행한 뒤 theme을 `blowfish`로 설정한다.

```Powershell
theme = "blowfish"
```

{{< figure src="img/edit-hugo-toml-theme.png" alt="Edit hugo.toml" >}}

---

## 5. Hugo 서버 실행

기본적인 모든 준비는 끝났기 때문에 정상적으로 블로그가 실행되는지 터미널에서 아래 명령어를 입력하여 로컬 서버를 실행해봅니다.

```PowerShell
hugo server
```

브라우저를 열고 http://localhost:1313/ 에 접속해 보세요. Blowfish 테마의 기본 레이아웃이 보인다면 성공입니다.

{{< figure src="img/run-blowfish-server.png" alt="Run Hugo Blowfish Blog Server" >}}

---

## 6. 마치며

이제 블로그의 뼈대가 완성되었습니다. 하지만 아직은 기본 설정 상태이기 때문에 메뉴도 없고, 언어도 영어이며 프로필 등 아무런 세팅이 안되있습니다..

다음 편에서는 본격적으로 한국어 설정, 프로필 추가, 메뉴 구성 등 블로그를 내 입맛에 맞게 커스터마이징하는 방법을 알아보겠습니다.
