---
title: "Hugo 블로그 관리: Blowfish 테마 업데이트 후 LanguageCode 경고 해결 방법 (v0.158.0 대응)"
slug: hugo-blowfish-update-locale
date: 2026-05-20T13:00:00+09:00
description: "Hugo v0.158.0 업데이트에 따라 폐기된 languageCode 설정을 신규 규격인 locale 및 label 속성으로 전환하여 터미널 경고를 해결하는 방법을 알아봅니다."
summary: "Hugo v0.158.0 및 Blowfish 테마 업데이트 후 발생하는 다국어 설정 경고(languageCode)를 최신 규격인 locale 및 label로 안전하게 마이그레이션하여 해결하는 가이드입니다."
categories: ["Hugo", "Web Development", "Tutorial"]
tags: ["Hugo", "Blowfish", "Theme", "Config", "Multi-language", "Locale", "VS Code"]
draft: false
---

정말 오랜만에 Hugo 블로그의 정적 테마인 **Blowfish** 를 업데이트했습니다.

기존에 사용하던 `v2.97.0` 버전에서 `v2.103.0` 버전으로 판올림을 진행했는데요.

업데이트 이후 로컬 서버를 구동하자마자 터미널에 이전에 보지 못했던 새로운 경고 메시지가 대거 출력되는 것을 확인했습니다.

겪은 경험을 공유하고자 게시글을 작성합니다.

---


## 1. 문제 상황: Deprecated 경고 발생

테마 업데이트 후 터미널에서 로컬 확인을 위해 `hugo server` 명령어를 실행했더니 다음과 같은 경고(WARN) 문구가 나타났습니다.

{{< figure src="img/01-hugo-deprecated-warn.png" alt="Hugo server 실행 시 languages.en.languageCode 경고 메시지가 터미널에 출력된 화면" >}}

```
WARN  deprecated: project config key languages.en.languageCode was deprecated in Hugo v0.158.0 and will be removed in a future release. Use languages.en.locale instead.
```

경고의 원인을 파악해 보니, 최신 Blowfish 테마가 요구하는 Hugo의 최소 버전이 `v0.158.0`으로 상향 조정되면서 발생한 문제였습니다.

Hugo `v0.158.0` 버전부터는 기존 다국어 설정에 사용되던 languageCode 속성이 폐기(Deprecated) 예정 처리되었으며, 향후 완전 삭제될 예정이므로 이를 locale 속성으로 대체하라는 지침입니다.

당장 블로그 빌드나 운영에 문제가 생기는건 아니지만, 추후 Hugo 버전을 더 올리게 되면 다국어 처리가 완전히 깨질 수 있기 때문에 미리 수정하기로 마음 먹었습니다.

---

## 2. 수정해야 할 파일 위치 확인

이 경고를 해결하기 위해서는 블로그 루트 디렉터리 내에 존재하는 다국어 설정 파일들을 수정해야 합니다. Blowfish 테마 구조 기준으로 설정 파일은 아래 경로에 위치해 있습니다.

{{< figure src="img/02-config-languages-folder.png" alt="Hugo 프로젝트의 config default 폴더 내에 languages.ko.toml 파일과 languages.en.toml 파일이 있는 경로 구조" >}}

- 한국어 설정 파일: `\config\_default\languages.ko.toml`

- 영어 설정 파일: `\config\_default\languages.en.toml`

만약 다른 언어를 추가로 서비스하고 있다면, 해당 언어의 TOML 파일도 동일한 방식으로 함께 수정해 주셔야 합니다.

---

## 3. VS Code를 이용한 코드 수정

수정 방법은 매우 간단합니다. 사용 중인 코드 편집기(VS Code 등)로 해당 파일들을 열어 매핑되는 키 이름을 최신 서식에 맞게 변경해 주기만 하면 됩니다.

### ① 수정전

기존 파일들은 아래와 같이 `languageCode`와 `languageName`으로 작성되어 있습니다.

{{< figure src="img/03-vscode-before-edit.png" alt="VS Code에서 languages.ko.toml 파일의 구버전 languageCode 및 languageName 설정 코드 화면" >}}

```toml
# config/_default/languages.en.toml
[en]
  languageCode = "en-us"
  languageName = "English"
  weight = 2
```

### ② 수정후

Hugo `v0.158.0` 가이드라인 및 Blowfish 메인 가이드에 따라 명칭을 아래와 같이 변경합니다. languageCode 대신 `locale`을, languageName 대신 `label`을 입력하면 됩니다.

{{< figure src="img/04-vscode-after-edit.png" alt="VS Code에서 languages.ko.toml 설정을 신버전 규격인 locale 및 label 속성으로 수정한 화면" >}}

```toml
# config/_default/languages.en.toml
[en]
  locale = "en-us"
  label = "English"
  weight = 2
```

---

## 4. 결과 확인

저장 후, 다시 터미널을 열어 로컬 서버를 실행해 봅니다.

{{< figure src="img/05-hugo-server-success.png" alt="다국어 속성 수정 후 Hugo server를 실행했을 때 경고 메시지 없이 깔끔하게 컴파일 완료된 터미널 화면" >}}

```
hugo server
```

이전과 달리 지저분하게 출력되던 WARN deprecated 관련 메시지가 말끔히 사라지고, 아주 깔끔하게 서버가 구동되는 것을 확인할 수 있습니다.

---

## 마치며

정적 사이트 생성기인 Hugo나 Blowfish 같은 다기능 테마는 메이저 업데이트가 발생할 때마다 구성 서식(Configuration Schema)이 조금씩 변한다고 합니다.

경고 문구가 떴을 때 방치하기보다는, 미리미리 규격에 맞게 변경해주는 것이 장기적인 유지 보수 관리에 좋을 것 같습니다.

마지막으로 참고한 가이드 안내드리고 이만 물러가겠습니다.

- Blowfish 공식 디스커션: [Blowfish Discussion](https://github.com/nunocoracao/blowfish/discussions/2944)

- Hugo 공식 설정 가이드: [Hugo Language Configuration](https://gohugo.io/configuration/languages/)