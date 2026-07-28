---
title: "Hugo Blowfish 블로그에 Microsoft Clarity 적용하는 방법"
slug: "hugo-blowfish-microsoft-clarity"
date: 2026-07-27T12:00:00+09:00
description: "Microsoft Clarity의 주요 기능과 장점을 살펴보고 Hugo Blowfish 블로그에 추적 코드를 적용하는 방법을 정리합니다."
summary: "방문자가 블로그에서 어디를 클릭하고 얼마나 스크롤하는지 확인할 수 있는 Microsoft Clarity를 Hugo Blowfish 블로그에 연결하는 방법을 소개합니다."
categories: ["Hugo", "Operation"]
tags: ["Microsoft Clarity", "Hugo", "Blowfish", "웹 분석", "히트맵"]
draft: false
---

블로그를 운영하다 보면 방문자 수뿐만 아니라 **방문자가 어떤 글을 읽고, 어디를 클릭하며, 어느 지점에서 페이지를 벗어나는지** 궁금할 때가 있습니다.

Google Analytics가 방문자 수와 유입 경로 같은 수치를 확인하는 데 유용하다면, [Microsoft Clarity](https://clarity.microsoft.com/)는 방문자의 실제 행동을 화면으로 살펴보는 데 유용한 도구입니다.

이번 글에서는 Microsoft Clarity의 주요 기능과 장점을 간단히 살펴보고, Hugo Blowfish 블로그에 직접 적용해보겠습니다.

---

## 1. Microsoft Clarity란?

Microsoft Clarity는 웹사이트 방문자의 행동을 분석할 수 있는 도구입니다. 무료로 사용할 수 있으며, 대표적으로 다음 기능을 제공합니다.

- **세션 녹화**: 방문자가 페이지를 이동하고 클릭하는 과정을 재생합니다.
- **히트맵**: 클릭 위치와 스크롤 범위를 시각적으로 보여줍니다.
- **대시보드**: 방문자의 기기, 유입 경로, 인기 페이지 등을 한눈에 확인합니다.
- **AI 요약**: 수집된 행동 데이터에서 주요 특징과 개선점을 요약합니다.

단순한 방문자 수를 넘어, 방문자가 블로그를 **어떻게 이용하는지** 확인할 수 있다는 점이 가장 큰 특징입니다.

![Microsoft Clarity 소개 사이트](img/microsoft-clarity-dashboard.png)

---

## 2. Clarity를 적용하는 이유

블로그에 Clarity를 적용하면 글의 구성과 사용성을 개선할 때 실제 방문자 행동을 참고할 수 있습니다.

- 글의 어느 부분까지 읽는지 확인할 수 있습니다.
- 자주 클릭하는 링크와 버튼을 찾을 수 있습니다.
- 클릭되지 않는 요소나 불편한 이동 경로를 발견할 수 있습니다.
- PC와 모바일에서 나타나는 사용 패턴을 비교할 수 있습니다.

예를 들어 방문자가 글의 중간에서 대부분 이탈한다면 내용을 더 간결하게 다듬을 수 있고, 특정 링크를 자주 클릭한다면 관련 글이나 메뉴를 더 눈에 띄게 배치할 수 있습니다.

---

## 3. Clarity 프로젝트 만들기

먼저 Clarity에서 블로그를 분석할 프로젝트를 만듭니다.

1. [Microsoft Clarity](https://clarity.microsoft.com/)에 접속해 로그인합니다.
2. **새 프로젝트(New project)**를 선택합니다.
3. 프로젝트 이름과 블로그 주소를 입력합니다.

![Microsoft Clarity 프로젝트 생성](img/clarity-create-project.png)

4. 프로젝트 생성 후 **Getting Started**에서 **Install manually > Get tracking code**를 선택한다.

![Microsoft Clarity 추적 코드 생성](img/clarity-install-manually.png)

5. **Copy to clipboard**를 클릭하여 코드를 복사합니다.

![Microsoft Clarity 추적 코드 복사](img/clarity-copy-tracking-code.png)

프로젝트마다 추적 코드가 다르기 떄문에 Clarity에서 발급된 코드를 그대로 사용해야 합니다.

---

## 4. Blowfish 블로그에 추적 코드 추가하기

Clarity 추적 코드는 웹사이트의 `<head>` 영역에 추가해야 합니다.

Blowfish 테마는 별도의 파일을 이용해 `<head>`에 코드를 추가할 수 있습니다. 블로그 프로젝트에 아래 파일을 만듭니다.

```text
layouts/partials/extend-head.html
```

그리고 Clarity에서 복사한 추적 코드를 파일에 붙여넣습니다.

```html
<!-- Microsoft Clarity -->
<script type="text/javascript">
  (function(c,l,a,r,i,t,y){
    c[a]=c[a]||function(){(c[a].q=c[a].q||[]).push(arguments)};
    t=l.createElement(r);t.async=1;t.src="https://www.clarity.ms/tag/"+i;
    y=l.getElementsByTagName(r)[0];y.parentNode.insertBefore(t,y);
  })(window, document, "clarity", "script", "YOUR_PROJECT_ID");
</script>
```

위 예시의 `YOUR_PROJECT_ID` 부분은 실제로 발급받은 프로젝트 ID로 바꿔야 합니다. 가장 안전한 방법은 예시 코드를 수정하기보다 **Clarity에서 복사한 전체 코드를 그대로 붙여넣는 것**입니다.

테마 내부의 파일을 직접 수정할 필요는 없습니다. 프로젝트의 `layouts/partials/extend-head.html`을 사용하면 테마를 업데이트한 뒤에도 설정을 유지하기 쉽습니다.

자세한 내용은 [Blowfish의 Head and Footer 공식 문서](https://blowfish.page/docs/partials/#head-and-footer)에서 확인할 수 있습니다.

![VS Code로 Microsoft Clarity 추적 코드 삽입](img/blowfish-extend-head-clarity.png)

---

## 5. 적용 결과 확인하기

파일을 저장한 뒤 블로그를 배포하고 직접 몇 개의 페이지를 이동하거나 스크롤해봅니다.

이후 Clarity 프로젝트의 대시보드나 **Recordings** 메뉴에서 데이터가 수집되는지 확인합니다. 바로 확인되지 않는다면 잠시 기다린 뒤 다시 확인합니다.

조금 더 확실하게 확인하려면 브라우저 개발자 도구의 **Network** 탭에서 `collect`를 검색해 `clarity.ms/collect` 요청이 전송되는지 살펴볼 수도 있습니다.

![Clarity 대시보드에 실시간 사용자가 표시된 화면](img/clarity-installation-result.png)

---

## 적용 전 확인할 점

Clarity는 방문자 행동과 쿠키를 이용하는 분석 도구이므로 블로그의 개인정보 처리방침과 쿠키 동의가 필요한 환경인지 확인해야 합니다. 특히 해외 방문자를 대상으로 운영한다면 관련 정책을 함께 검토하는 것이 좋습니다.

또한 Microsoft는 기본적으로 민감한 콘텐츠를 마스킹한다고 안내하지만, 실제 세션 녹화 화면에서 의도하지 않은 정보가 보이지 않는지도 확인하는 것을 권장합니다.

---

## 마치며

Microsoft Clarity를 이용하면 방문자 수만으로는 알기 어려웠던 클릭, 스크롤, 이탈 행동을 직접 확인할 수 있습니다.

Hugo Blowfish에서는 `extend-head.html` 파일 하나만 추가하면 되므로 적용 방법도 어렵지 않습니다. 데이터가 어느 정도 쌓이면 히트맵과 세션 녹화를 살펴보면서 글의 구성과 블로그 메뉴를 조금씩 개선해볼 예정입니다.

## 참고 자료

- [Microsoft Clarity 공식 사이트](https://clarity.microsoft.com/)
- [Microsoft Clarity 설치 안내](https://learn.microsoft.com/en-us/clarity/setup-and-installation/clarity-setup)
- [Blowfish Head and Footer 설정](https://blowfish.page/docs/partials/#head-and-footer)
