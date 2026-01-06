---
title: "Hugo 블로그 만들기 "
slug: hugo-project-theme
date: 2026-01-07T22:00:00+09:00
description: "Hugo로 새로운 블로그 프로젝트를 생성하고, Git Submodule을 이용해 Blowfish 테마를 설치하는 방법을 단계별로 알아봅니다."
series: Hugo 블로그 만들기
series_order: 2
categories: ["Hugo", "Web Development", "Tutorial"]
tags: ["Hugo", "SSG", "Blog", "Blowfish", "Theme", "Git", "Submodule", "Config"]
showTableOfContents: true
draft: true
---

지난 1편에서 윈도우 환경에 Hugo(Extended 버전) 설치를 완료했습니다. 이제 본격적으로 나만의 블로그 프로젝트를 생성하고, 아름답고 기능 강력한 테마인 **Blowfish**를 입혀볼 차례입니다.

## 1. 새 Hugo 프로젝트 생성

원하는 폴더(예: `C:\Project`)로 이동한 뒤, 터미널에서 아래 명령어를 입력하여 새로운 사이트를 생성합니다. 저는 블로그 이름을 `my-blog`로 정했습니다.

```powershell
hugo new site my-blog
```
