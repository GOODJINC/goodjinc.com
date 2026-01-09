---
title: "Hugo 블로그 만들기 (5): 깃허브(GitHub) 업로드 및 클라우드플레어 배포"
slug: hugo-deployment-cloudflare
date: 2026-01-09T08:50:00+09:00
description: "로컬에서 완성한 Hugo 블로그를 GitHub에 업로드하고, Cloudflare Pages를 통해 전 세계에 무료로 배포하는 전 과정을 상세히 설명합니다."
series: ["Hugo 블로그 만들기"]
series_order: 5
categories: ["DevOps", "Deployment"]
tags: ["GitHub", "Cloudflare Pages", "Hosting", "Custom Domain"]
draft: false
# Thumbnail : https://pixabay.com/illustrations/server-servers-data-computer-5451985/
---

지난 4편까지의 과정을 통해 나만의 블로그를 완성했습니다. 하지만 현재 이 블로그는 나의 컴퓨터 안(`localhost:1313`)에서만 존재하는 상태입니다.

이제 이 결과물을 **깃허브(GitHub)** 에 올리고, **클라우드플레어 페이지(Cloudflare Pages)** 라는 서비스를 이용해 전 세계 누구나 접속할 수 있는 실제 웹사이트로 배포해 보겠습니다.

저는 **클라우드플레어**를 이용해 개인 도메인을 적용할 예정입니다. 그렇기 때문에 깃허브 페이지나 Netlify나 Vercel 등을 이용하신다면 일부 구성 및 순서가 다를 수 있습니다.

---

## 1. GitHub 저장소(Repository) 생성

먼저 블로그 소스 코드를 안전하게 보관하고 배포의 핵심 역할을 할 **GitHub 리포지토리**가 필요합니다.

1. [GitHub](https://github.com/)에 로그인한 뒤 **New Repository**를 클릭합니다.
2. 저장소 이름(예: `my-blog`)을 정하고 생성합니다.
3. 생성 후 화면에 나타나는 **저장소 주소(URL)**를 복사해 둡니다. (예: `https://github.com/GOODJINC/my-blog.git`)

{{< figure src="img/github-new-repository.png" alt="Github New Repository" >}}

{{< alert >}}
개인 도메인을 사용하지 않고, 깃허브 페이지에서 기본 제공하는 `[ID].github.io` 도메인을 사용하고 싶다면 `공개 여부(Visibility)`를 `공개(Public)`으로 설정합니다. 저는 개인 도메인을 적용할 예정이기에 `비공개(Private)`로 설정했습니다. </br>
첫 블로그이다보니 여러 테스트를 진행중이라 소스 코드를 공개하지 못하고 있습니다. 어느정도 정리되는대로 깃허브 리포지토리를 공개로 바꿀 생각을 하고 있습니다.
{{< /alert >}}

---

## 2. 로컬 소스 코드 업로드

이제 내 컴퓨터에 있는 블로그 파일들을 GitHub에 올릴 차례입니다.

### ① .gitignore 확인

GitHub에 올릴 때, Hugo가 생성한 결과물인 `public` 폴더는 올릴 필요가 없습니다. Cloudflare가 서버에서 직접 빌드해주기 때문입니다.

`.gitignore`이 없다면 루트 폴더에서 `.gitignore` 파일을 생성 후 아래 내용을 추가해주세요.

```text
public/
resources/_gen/
.hugo_build.lock
```

{{< alert >}}
클라우드 플레어가 아니라 깃허브 페이지 등을 이용하신다면 `public` 폴더가 필요할 수 있습니다. 사용하실 서비스에 따라 `.gitignore` 구성이 달라질 수 있으니 주의해주세요.
{{< /alert >}}

### ② Git 명령어로 업로드

루트 폴더에서 터미널 실행 후 아래 명령어를 순서대로 입력합니다.

```Powershell
git add .
git commit -m "First commit: Hugo blog with Blowfish theme"
git branch -M main
git remote add origin [아까 복사한 저장소 주소(예: https://github.com/GOODJINC/my-blog.git)]
git push -u origin main
```

이후 Github > my-blog 레포지토리에 접속하여 정상적으로 업로드 되었는지 확인해봅니다.

---

## 3. Cloudflare Pages와 Github 연결

이제 Cloudflare가 GitHub의 코드를 감지해서 자동으로 웹사이트를 만들어주도록 설정해야 합니다.

① Cloudflare 대시보드에 접속하여 로그인한 뒤, 우측 상단의 `추가(+)` 아이콘을 클릭한 뒤 `Pages`를 클릭합니다.

{{< figure src="img/cloudflare-new-pages.png" alt="Create Pages in Cloudflare" >}}

② `기존 Git 리포지토리 가져오기(Import an existing Git repository)`를 선택합니다. (저희는 이미 깃허브 리포지토리를 만들었기 때문에 해당 방식을 사용합니다.)

{{< figure src="img/cloudflare-import-git-repository.png" alt="Import an existing Git repository in Cloudflare" >}}

③ 깃허브에 연결하여 블로그 리포지토리와 연동하는 설정을 진행합니다.

{{< figure src="img/cloudflare-connect-github-repository.png" alt="Connect Github Repository" >}}

④ 전 단계에서 추가 및 연동한 리포지토리를 선택한 뒤 `설정 시작(Begin Setup)`을 클릭한다.

{{< figure src="img/cloudflare-select-github-repository.png" alt="Select Repository and Begin Setup" >}}

---

## 4. 빌드 설정

이 단계가 가장 중요합니다. 아래 내용을 정확히 입력해야 빌드 에러가 발생하지 않습니다.

- **프레임워크 미리 설정(Framework preset)**: Hugo
- **빌드 명령(Build command)**: hugo --gc --minify
- **빌드 출력 디렉터리(Build output directory)**: public

{{< figure src="img/cloudflare-build-settings.png" alt="Build Settings in Cloudflare" >}}

모든 설정이 끝났다면 **저장 및 배포(Save and Deploy)** 를 클릭합니다.

{{< figure src="img/cloudflare-building-deploying.png" alt="Repository Building and Deploying" >}}

잠시 기다리면 배포가 끝나고 성공한 모습을 확인할 수 있습니다. 그리고 내 블로그에 접속 가능한 주소를 할당받은 것도 확인할 수 있습니다.

{{< figure src="img/cloudflare-building-success.png" alt="Success Building and Deploying" >}}


---

## 5. 커스텀 도메인 연결 (goodjinc.com)

배포가 완료되면 `my-blog.pages.dev`와 같은 기본 주소가 할당됩니다. 하지만 본격적인 블로거로 활동하기 위해 개인 도메인을 연결하는 것이 좋습니다.

① Cloudflare Pages 프로젝트 화면에서 `사용자 설정 도메인(Custom domains)` 탭으로 이동합니다.

{{< figure src="img/cloudflare-deployments-tab.png" alt="Deployment Tab in Cloudflare" >}}

② `사용자 설정 도메인 설정(Set up a custom domain)`을 누르고 나만의 도메인(예: goodjinc.com)을 입력합니다.

{{< figure src="img/cloudflare-add-custom-domain.png" alt="Add Custom Domain in Cloudflare" >}}

③ Cloudflare가 자동으로 DNS 레코드를 갱신하도록 승인하면 모든 절차가 완료됩니다.

개인 도메인을 구매 및 관리할 수 있는 많은 서비스들이 있겠지만, 저는 [호스팅케이알](https://www.hosting.kr/)이라는 서비스를 이용하여 도메인은 구매 및 관리하고 있습니다.

---

## 6. 마치며

이제 나만의 작고 소중한 블로그에 많은 분들이 접속할 수 있게 되었습니다!

앞으로 PC에서 새로운 글을 쓰고 `git push`만 하면, Cloudflare가 이를 자동으로 감지하여 몇 분 안에 전 세계로 배포해 줄 것입니다.

배포는 끝났지만, 아직 할 일이 하나 더 남았습니다. 작성한 글들이 네이버나 구글 검색 결과에 나오도록 만드는 일입니다.

마지막 편인 다음 시간에는 `네이버/구글 검색 등록 방법`과 `구글 애널리틱스 연결 방법`에 대해 알아보겠습니다.
