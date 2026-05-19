---
title: "CIMON SCADA 삭제 후에도 남아있는 우클릭 메뉴 찌꺼기 제거하기"
slug: "windows-11-cimon-scada-context-menu-cleanup"
date: 2026-05-19T12:30:00+09:00
description: "CIMON SCADA를 삭제해도 마우스 우클릭 '새로 만들기' 목록에 남아있는 불필요한 확장자들을 레지스트리로 일괄 삭제하는 방법을 소개합니다."
summary: "제어판에서 지워지지 않는 CIMON SCADA의 우클릭 메뉴 찌꺼기를 원클릭으로 청소해 보세요. 삭제 및 복구 레지스트리 파일을 모두 제공합니다."
categories: ["Tech"]
tags: ["Windows 11", "OS 설정", "생산성", "레지스트리", "SCADA"]
draft: false
---

산업용 자동화 소프트웨어인 **CIMON SCADA**를 사용하다가 프로그램을 제어판에서 정상적으로 삭제했음에도 불구하고, 바탕화면이나 탐색기에서 마우스 우클릭을 했을 때 **새로 만들기** 목록에 CIMON 관련 확장자들이 그대로 남아있는 경우가 있습니다.

이렇게 지저분하게 남은 컨텍스트 메뉴 찌꺼기들을 마주했을 때가 가장 찝찝할 때입니다. `.cmt`, `.bdx`, `.sch` 등 무려 11개나 되는 불필요한 확장자들이 메뉴를 차지하고 있으면 시각적으로도 번잡하고 작업 효율도 떨어집니다.

프로그램 자체는 삭제되었지만, Windows 레지스트리의 `HKEY_CLASSES_ROOT` 경로에 등록된 확장자 키들이 완전히 청소되지 않아 발생합니다.

그래서 이번 시간에는 **레지스트리 파일 수정**만으로 빠르게 CIMON SCADA의 우클릭 찌꺼기 메뉴들을 지우거나 다시 복원하는 방법을 소개합니다.

---

## 1. 레지스트리 파일로 간편하게 설정하기

일일이 레지스트리 편집기(`regedit`)를 열어 11개의 확장자를 찾아 지우는 것은 매우 번거롭습니다. 간편한 적용을 원하시는 분들을 위해 `원클릭 설정 파일`을 준비했습니다. 우선 어떤 코드로 구성되어 있는지 소개합니다.

### ① 찌꺼기 확장자 일괄 삭제하기

CIMON SCADA가 남겨둔 마우스 오른쪽 클릭 메뉴 내의 확장자 11종(`.cmt`, `.bdx`, `.gsh`, `.hkd`, `.PGX`, `.prj`, `.rcp`, `.rpt`, `.sch`, `.scx`, `.WGX`)을 시스템에서 완전히 제거하는 레지스트리 코드입니다.

파일 다운로드 후 더블클릭하여 파일을 실행하면 찌꺼기들이 삭제된 것을 확인할 수 있습니다.

만약 즉시 적용되지 않았다면 [3. 변경 사항 즉시 반영하기 (탐색기 재시작)](#restart-explorer) 단계를 따라 Windows 탐색기를 재시작하면 적용됩니다.

**소스 코드**:

```reg
Windows Registry Editor Version 5.00

[-HKEY_CLASSES_ROOT\.cmt]
[-HKEY_CLASSES_ROOT\.bdx]
[-HKEY_CLASSES_ROOT\.gsh]
[-HKEY_CLASSES_ROOT\.hkd]
[-HKEY_CLASSES_ROOT\.PGX]
[-HKEY_CLASSES_ROOT\.prj]
[-HKEY_CLASSES_ROOT\.rcp]
[-HKEY_CLASSES_ROOT\.rpt]
[-HKEY_CLASSES_ROOT\.sch]
[-HKEY_CLASSES_ROOT\.scx]
[-HKEY_CLASSES_ROOT\.WGX]
```

**파일 다운로드**:

- <a href="delete-cimon-scada-extensions.reg" download="delete-cimon-scada-extensions.reg" class="btn btn-primary" style="text-decoration: none; display: inline-block;">CIMON SCADA 확장자 제거 파일 다운로드</a>

> [!TIP] **파일 실행 후 할 행동**
> 파일 다운로드 및 실행 후 [3. 변경 사항 즉시 반영하기 (탐색기 재시작)](#restart-explorer) 단계를 따라 Windows 탐색기를 재시작해주세요.

### ② 확장자 기본 키 복구하기 (만약을 위한 백업)

스카다를 쓸 때 마우스 오른쪽 클릭 후 확장자를 생성했던 적이 없었기 때문에 아마 복원할 일은 없을 것 같습니다.

하지만 혹시라도 나중에 CIMON SCADA를 다시 설치하게 된다면 다시 복원되겠지만 원래 상태로 돌아오지 않을 때를 위한 레지스트리 코드입니다.

파일 다운로드 후 더블클릭하여 파일을 실행하면 해당 확장자들의 기본 키 구조가 다시 생성됩니다.

**소스 코드**:

```reg
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\.cmt]
[HKEY_CLASSES_ROOT\.bdx]
[HKEY_CLASSES_ROOT\.gsh]
[HKEY_CLASSES_ROOT\.hkd]
[HKEY_CLASSES_ROOT\.PGX]
[HKEY_CLASSES_ROOT\.prj]
[HKEY_CLASSES_ROOT\.rcp]
[HKEY_CLASSES_ROOT\.rpt]
[HKEY_CLASSES_ROOT\.sch]
[HKEY_CLASSES_ROOT\.scx]
[HKEY_CLASSES_ROOT\.WGX]
```

**파일 다운로드**:

- <a href="restore-cimon-scada-extensions.reg" download="restore-cimon-scada-extensions.reg" class="btn btn-primary" style="text-decoration: none; display: inline-block;">CIMON SCADA 확장자 복원 파일 다운로드</a>

---

## 2. 명령 프롬프트(CMD)로 직접 설정하기

파일 다운로드가 찜찜하고 걱정이 된다면, **CMD(명령 프롬프트)** 에서 아래 명령어를 복사하여 직접 입력하셔도 동일하게 하나씩 삭제할 수 있습니다.

### ① CMD 관리자 권한으로 실행하기

레지스트리의 HKEY_CLASSES_ROOT 영역을 제어해야 하므로, 윈도우 시작 메뉴에서 CMD를 검색한 뒤 반드시 `[관리자 권한으로 실행]`을 선택하여 실행합니다.

### ② 확장자 키 직접 삭제하기

아래 명령어를 전체 복사하여 한 번에 입력(붙여넣기)한 뒤 Enter를 눌러 실행해 줍니다.

```
reg delete "HKCR\.cmt" /f
reg delete "HKCR\.bdx" /f
reg delete "HKCR\.gsh" /f
reg delete "HKCR\.hkd" /f
reg delete "HKCR\.PGX" /f
reg delete "HKCR\.prj" /f
reg delete "HKCR\.rcp" /f
reg delete "HKCR\.rpt" /f
reg delete "HKCR\.sch" /f
reg delete "HKCR\.scx" /f
reg delete "HKCR\.WGX" /f
```

---

## 3. 변경 사항 즉시 반영하기 (탐색기 재시작) {#restart-explorer}

레지스트리를 수정했다고 해서 새로 만들기 목록에서 확장자들이 즉시 사라지지 않을 수 있습니다.

그럴 때는 컴퓨터를 재부팅하거나, 아래 방법으로 윈도우 탐색기(Explorer)를 재시작해야 캐시가 초기화됩니다.

① `Ctrl + Shift + Esc`를 눌러 작업 관리자를 엽니다.

② `Windows 탐색기 프로세스`를 찾아 마우스 우클릭 후 `[다시 시작]`을 클릭합니다.

③ 또는 관리자 권한 권한의 `CMD` 창에 아래 명령어를 입력하여 강제로 탐색기를 껐다 켜 줍니다.

```
taskkill /f /im explorer.exe & start explorer.exe
```

## 마치며

프로그램을 정상적인 경로로 언인스톨했음에도 시스템 내부에 찌꺼기 데이터를 남겨두어 사용자가 직접 레지스트리를 건드리게 만드는 점은 다소 아쉽습니다.

싸이몬 공식 웹사이트의 Q&A 게시판에 이미 작년에 올라온 질문이 있는데 별도 매뉴얼을 제공하지 않는 것 같습니다.

물론 제대로 삭제가 안되는게 저처럼 소수의 사례일 수 있지만, 이런 부분도 대응해줬으면 했는데 아쉽네요.

이런 사례처럼 개선된 버전이 나오지 않거나 만약 다른 프로그램에서도 동일한 문제가 발생한다면 해당 방법으로 대처할 수 있을 것 같습니다.

이상 간단한 레지스트리 정리만으로도 Windows 환경을 훨씬 깔끔하게 유지할 수 있는 방법을 소개해드렸습니다.