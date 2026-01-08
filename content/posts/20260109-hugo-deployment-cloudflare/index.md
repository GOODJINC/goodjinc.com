---
title: "Hugo 블로그 만들기 (5): 깃허브(GitHub) 업로드 및 클라우드플레어 배포"
slug: hugo-deployment-cloudflare
date: 2026-01-08T08:50:00+09:00
description: "로컬에서 완성한 Hugo 블로그를 GitHub에 업로드하고, Cloudflare Pages를 통해 전 세계에 무료로 배포하는 전 과정을 상세히 설명합니다."
series: ["Hugo 블로그 만들기"]
series_order: 5
categories: ["DevOps", "Deployment"]
tags: ["GitHub", "Cloudflare Pages", "CI/CD", "Hosting", "Custom Domain"]
draft: true
# Thumbnail :
---

지난 4편까지의 과정을 통해 나만의 멋진 블로그를 완성했습니다. 하지만 현재 이 블로그는 나의 컴퓨터 안(`localhost:1313`)에서만 존재하는 상태입니다.

이제 이 결과물을 **깃허브(GitHub)**에 올리고, **클라우드플레어 페이지(Cloudflare Pages)**라는 서비스를 이용해 전 세계 누구나 접속할 수 있는 실제 웹사이트로 배포해 보겠습니다.

---

## 1. GitHub 저장소(Repository) 생성

먼저 블로그 소스 코드를 안전하게 보관하고 배포의 핵심 역할을 할 **GitHub 리포지토리**가 필요합니다.

1. [GitHub](https://github.com/)에 로그인한 뒤 **New Repository**를 클릭합니다.
2. 저장소 이름(예: `my-blog`)을 정하고 생성합니다.
3. 생성 후 화면에 나타나는 **저장소 주소(URL)**를 복사해 둡니다. (예: https://github.com/GOODJINC/my-blog.git)

{{< alert >}}
개인 도메인을 사용하지 않고, 깃허브 페이지에서 기본 제공하는 `[ID].github.io` 도메인을 사용하고 싶다면 `공개 여부(Visibility)`를 `공개(Public)`으로 설정합니다. 저는 개인 도메인을 적용할 예정이기에 `비공개(Private)`로 설정했습니다.
{{< /alert >}}

---

## 2. 로컬 소스 코드 업로드

이제 내 컴퓨터에 있는 블로그 파일들을 GitHub에 올릴 차례입니다.

### ① .gitignore 확인

GitHub에 올릴 때, Hugo가 생성한 결과물인 `public` 폴더는 올릴 필요가 없습니다. Cloudflare가 서버에서 직접 빌드해주기 때문입니다. 루트 폴더의 `.gitignore` 파일에 아래 내용이 있는지 확인하십시오.

```text
public/
resources/_gen/
.hugo_build.lock
```

### ② Git 명령어로 업로드

터미널에서 아래 명령어를 순서대로 입력합니다.

```Powershell
git add .
git commit -m "First commit: Hugo blog with Blowfish theme"
git branch -M main
git remote add origin [아까 복사한 저장소 주소]
git push -u origin main
```

---

## 3. Cloudflare Pages 배포 설정

이제 Cloudflare가 GitHub의 코드를 감지해서 자동으로 웹사이트를 만들어주도록 설정해야 합니다.

Cloudflare 대시보드에 접속하여 로그인합니다.

왼쪽 메뉴에서 Workers & Pages -> Create application -> Pages -> Connect to Git을 선택합니다.

내 GitHub 계정을 연결하고, 방금 만든 my-blog 저장소를 선택한 뒤 Begin setup을 누릅니다.

---

## 4. 빌드 설정 (Build settings)

이 단계가 가장 중요합니다. 아래 내용을 정확히 입력해야 빌드 에러가 발생하지 않습니다.

- **Framework preset**: Hugo 선택
- **Build command**: hugo --gc --minify
- **Build output directory**: public

💡 환경 변수(Environment variables) 설정 (필수!)

Cloudflare의 기본 Hugo 버전은 낮을 수 있습니다. 우리가 사용 중인 최신 버전과 맞추기 위해 **Environment variables** 탭에서 아래 항목을 추가하십시오.

- **Variable name**: `HUGO_VERSION`
- **Value**: `0.154.2` (본인이 설치한 hugo version 결과와 동일하게 입력)

모든 설정이 끝났다면 **Save and Deploy**를 클릭합니다.

---

## 5. 커스텀 도메인 연결 (goodjinc.com)

배포가 완료되면 my-blog.pages.dev와 같은 기본 주소가 할당됩니다. 하지만 전문적인 블로그를 위해 개인 도메인을 연결하는 것이 좋습니다.

① Cloudflare Pages 프로젝트 화면에서 Custom domains 탭으로 이동합니다.

② Set up a custom domain을 누르고 보유하신 도메인(예: goodjinc.com)을 입력합니다.

③ Cloudflare가 자동으로 DNS 레코드를 갱신하도록 승인하면 모든 절차가 완료됩니다.

---

## 6. 마치며

이제 당신의 블로그는 살아있는 웹사이트가 되었습니다! 앞으로 GitHub에 새로운 글을 쓰고 `git push`만 하면, Cloudflare가 이를 자동으로 감지하여 몇 분 안에 전 세계로 배포해 줄 것입니다. (이것이 바로 현대적인 배포 방식인 CI/CD입니다.)

배포는 끝났지만, 아직 할 일이 하나 더 남았습니다. 내 소중한 글들이 네이버나 구글 검색 결과에 잘 나오도록 만드는 일이죠.

마지막 편인 다음 시간에는 **검색엔진 최적화(SEO)**와 네이버/구글 검색 등록 방법을 알아보겠습니다.
