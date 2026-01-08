---
title: "Hugo 블로그 만들기 (1): 개발 환경 구축"
slug: hugo-install-windows
date: 2026-01-06T22:28:03+09:00
description: 윈도우(Windows) 환경에서 Hugo Extended 버전을 설치하고 블로그 개발 환경을 구축하는 방법을 다룹니다.
series: ["Hugo 블로그 만들기"]
series_order: 1
categories: ["DevOps", "Tutorial"]
tags: ["Hugo", "Windows", "Environment Setup", "SSG"]
draft: false
---

개발을 막 시작하는 입장에서 나만의 지식과 경험을 정리하고 공유할 공간이 필요했습니다. 왜냐면 저 역시 많은 지식들을 다른 분들에게서 얻었기 때문입니다.

네이버 블로그(Naver Blog)나 티스토리(Tistory), 벨로그(Velog) 등 많은 플랫폼들이 있지만, 커스터마이징의 한계와 데이터 소유권을 온전히 내가 가지고 싶다는 욕심에 **정적 사이트 생성기(SSG, Static Site Generator)** 인 **Hugo**를 선택하게 되었습니다.

우선 첫 시리즈로 휴고(Hugo) 블로그를 만드는 방법과 시행착오에 대해 제작할 예정입니다. **Hugo** 제작 환경 세팅부터 **Blowfish 테마** 적용, 그리고 **Cloudflare Pages**를 이용하여 개인 도메인을 적용하는 방법까지 블로그를 구축하는 전 과정을 기록할 예정입니다.

우선 윈도우 11(Windows 11) 환경에서의 개발 환경 구축 방법을 소개합니다.

---

## 1. Hugo를 선택한 이유

- **압도적인 속도:** Go 언어로 작성되어 빌드 속도가 타 SSG(Jekyll, Hexo 등) 대비 월등히 빠릅니다.
- **유연성:** 마크다운(Markdown) 기반으로 글을 작성하며, 테마 커스터마이징이 자유롭습니다.
- **무료 호스팅:** 정적 HTML 파일만 생성하기 때문에 GitHub Pages나 Cloudflare Pages에 무료로 배포할 수 있습니다.

---

## 2. 블로그 제작을 위한 툴 설치

원활한 블로그 구축과 운영을 위해 아래 프로그램들을 설치했습니다. 개발 환경 구축을 위해 사전 설치해주시면 됩니다. [Hugo 공식 매뉴얼](https://gohugo.io/installation/windows/)에서 더 자세한 정보도 확인하실 수 있습니다.

### 1) Visual Studio Code

커서(Cursor) 등 다양한 코드 편집기가 있지만 호환성이 가장 뛰어나고 다양한 플러그인 지원, 많은 사용 사례들이 있기 때문에 선택했습니다. 아직 잘 모르기 때문에 가장 많이 사용하는걸 설치해줍니다.

- [VS Code 다운로드](https://code.visualstudio.com/)

### 2) Git

버전 관리와 배포를 위해 필수 툴입니다. 저는 깃허브(GitHub)에서 관리할 예정이기 때문에 필수로 설치합니다.

- [Git for Windows 다운로드](https://git-scm.com/install/windows)

---

## 3. Hugo 설치하기 (중요)

Hugo 블로그 운영을 위해서는 당연히 Hugo 설치가 필요하겠죠. 미리 빌드된 바이너리를 이용하는 방식과 패키지 매니저를 이용한 방식이 있습니다.

Chocolatey이나 Scoop과 같이 윈도우 개발 도구의 편리한 설치를 위한 패키지 매니저를 이용하는 방식이 있지만, 저는 아직 사용해본 적도 없고 잘 모르기 때문에 **미리 빌드된 바이너리**를 이용하여 직접 설치하는 방식으로 진행하겠습니다.

패키지 매니저를 이용하실 분은 [공식 매뉴얼](https://gohugo.io/installation/windows/#package-managers)을 참고해주세요.

### 1) 미리 빌드된 바이너리로 Hugo 설치하기

Hugo는 일반 버전과 **Extended** 버전이 있습니다.

제가 사용할 **Blowfish** 테마를 비롯하여 최신 기능(SCSS/PostCSS 처리 등)을 활용하는 테마들은 Extended 버전이 필수입니다. 그렇기 때문에 반드시 Hugo Extended 버전을 설치해주시면 됩니다.

① [Hugo Binary 다운로드](https://github.com/gohugoio/hugo/releases/latest) 페이지에서 원하는 에디션, 운영 체제 등에 맞는 압축 파일을 다운로드합니다. 저는 `hugo_extended_0.154.2_windows-amd64.zip`을 다운로드 했습니다.

② 압축파일을 해제한 뒤 `C:\Hugo\bin` 폴더에 위치시킵니다.

{{< figure src="img/hugo-bin-folder.png" alt="Hugo Bin Folder Example" >}}

③ Win + R키를 누른 뒤 `sysdm.cpl`을 입력한 뒤 시스템 속성 > 고급 > 환경 변수에서 Hugo 폴더를 PATH 환경 변수에 추가합니다.

### 2) Hugo 설치 확인하기

터미널(Terminal)이나 파워셸(PowerShell)에서 아래 명령어를 입력하여 정상적으로 설치되었는지 확인합니다.

```powershell
hugo version
```

명령어 실행 후 아래와 같이 `+extended`라는 문구가 포함되어 있어야 합니다.

```powershell
hugo v0.154.2-f66d0944461 ... +extended windows/amd64 BuildDate= ...
```

{{< figure src="img/terminal-command.png" alt="hugo version Terminal Command" >}}

이렇게 되면 Hugo 블로그 개발 및 운영을 위한 사전작업은 끝났습니다.

다음 편에는 실제 프로젝트를 생성한 뒤 Blowfish 테마를 적용하는 방법을 소개하겠습니다.
