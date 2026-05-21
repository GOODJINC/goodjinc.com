---
title: "Cloudflare Pages: Hugo 블로그 배포 실패 (can't evaluate field Locale) 해결 방법"
slug: cloudflare-pages-hugo-build-failed-locale
date: 2026-05-21T12:00:00+09:00
description: "Cloudflare Pages에서 최신 Blowfish 테마 적용 후 발생하는 Hugo 빌드 에러 원인을 분석하고, HUGO_VERSION 환경 변수 설정을 통해 배포 실패를 해결하는 방법을 알아봅니다."
summary: "Blowfish 테마 업데이트 후 Cloudflare Pages에서 'can't evaluate field Locale' 에러로 빌드가 실패할 때, 환경 변수를 지정하여 Hugo 버전을 강제로 올리는 해결 가이드입니다."
categories: ["Hugo", "Web Development", "Cloudflare"]
tags: ["Hugo", "Blowfish", "Cloudflare Pages", "Build Error", "Deployment", "Environment Variable"]
draft: false
---

최신 Blowfish 테마 규격에 맞춰 다국어 설정을 수정한 뒤 깃허브(GitHub)에 푸시를 진행했습니다. 

로컬 환경(`hugo server`)에서는 아무런 경고 없이 깔끔하게 구동되는 것을 확인했기에 당연히 배포도 성공할 줄 알았으나, **Cloudflare Pages**에서 빌드가 실패(`exit code 1`)하는 문제가 발생했습니다.

로그 분석을 통해 파악한 원인과 가장 간단한 해결 방법을 공유합니다.

---

## 1. 문제 상황: Cloudflare 배포 로그 에러 발생

대시보드에서 배포 실패 로그를 확인해 보니 아래와 같은 에러 메시지가 출력되고 있었습니다.

{{< figure src="img/01-cloudflare-build-error.png" alt="Cloudflare Pages 빌드 로그에서 can't evaluate field Locale 에러로 인해 배포가 실패한 화면" >}}

```
2026-05-20T08:23:35.40313Z     WARN  Module "blowfish" is not compatible with this Hugo version: 0.158.0/0.161.1 extended; run "hugo mod graph" for more information.
...
2026-05-20T08:23:35.558814Z    ERROR render of "/404" failed: ... can't evaluate field Locale in type *langs.Language
...
2026-05-20T08:23:35.564486Z    Failed: Error while executing user command. Exited with error code: 1
```

로그를 자세히 뜯어보니 원인은 명확했습니다.

- 테마의 요구 사항: 업데이트된 Blowfish 테마는 내부적으로 `Hugo 0.158.0` 또는 `0.161.1 이상` 버전을 요구합니다.

- Cloudflare의 현재 환경: Cloudflare Pages의 기본 빌드 시스템이 사용 중인 Hugo 버전은 `v0.147.7`이었습니다.

로컬 컴퓨터는 최신 버전이라 문제가 없었지만, Cloudflare 서버의 Hugo 엔진 버전이 너무 낮다 보니 최신 테마의 구조(`.Site.Language.Locale` 등)를 해석하지 못해 빌드가 터진 것입니다.

---

## 2. 해결 방법: HUGO_VERSION 환경 변수 지정

이 문제는 Cloudflare Pages가 빌드를 수행할 때 최신 버전의 Hugo를 사용하도록 `환경 변수(Environment Variable)`를 심어주면 간단하게 해결됩니다.

### ① Cloudflare 프로젝트 설정 이동

[Cloudflare 대시보드](https://dash.cloudflare.com/ec5616c3d09ae19cb775579baf1ff640)에 로그인한 뒤, 해당 블로그 프로젝트를 선택합니다. 상단 메뉴에서 `설정` 탭을 누른 후, 왼쪽 사이드바에서 `변수 및 암호`를 클릭합니다.

{{< figure src="img/02-cloudflare-settings-env.png" alt="Cloudflare Pages 프로젝트 설정 메뉴에서 Environment variables 탭을 선택하는 화면" >}}

### ② 환경 변수 추가

`변수 및 암호` 영역에서 [추가] 버튼을 누르고 아래와 같이 입력합니다.

{{< figure src="img/03-cloudflare-add-variable.png" alt="Cloudflare 환경 변수 설정에 HUGO_VERSION 변수명과 0.161.1 값을 입력하는 화면" >}}

- 변수 이름: `HUGO_VERSION`

- 값: `0.161.1` (테마가 요구하는 안정적인 Hugo 버전)

입력을 마쳤다면 하단의 [저장] 버튼을 눌러 설정을 반영합니다.

### ③ 설정된 환경 변수 확인

아래와 같이 추가한 환경 변수가 잘 적용된 것을 확인할 수 있습니다.

변경된 내용은 다음 배포부터 적용되기 때문에 재배포를 해야 합니다.

{{< figure src="img/04-cloudflare-env-check.png" alt="Cloudflare 환경 변수 설정에 성공한 뒤 적용된 모습" >}}


---

## 3. 재배포 진행

설정을 저장한 후, 대시보드의 `최신` 탭으로 이동하여 [배포 다시 시도] 를 클릭하거나 깃허브에 빈 커밋을 푸시하여 빌드를 다시 트리거합니다.

{{< figure src="img/05-cloudflare-build-success.png" alt="환경 변수 적용 후 Cloudflare Pages 빌드가 성공적으로 완료된 화면" >}}

이전과 달리 지정한 고버전의 Hugo 엔진이 작동하면서, 에러 없이 깔끔하게 정적 파일 생성이 완료되고 성공적으로 배포가 마무리되는 것을 확인할 수 있습니다.

---

## 마치며

깃허브 페이지(GitHub Pages)나 클라우드플레어 페이지 같은 환경을 사용할 때, 로컬 엔진 버전과 서버 엔진 버전이 불일치하여 빌드가 깨지는 일은 꽤 흔하게 발생한다고 합니다.

특히 Blowfish처럼 발전이 빠른 테마를 판올림할 때는, 테마가 요구하는 최소 Hugo 버전을 확인하고 클라우드플레어 환경 변수도 함께 동기화해 주는 습관을 지니는 것이 좋을 것 같습니다.

저를 포함해 이번처럼 배포 실패로 답답하셨을 분들께 도움이 되었기를 바랍니다.