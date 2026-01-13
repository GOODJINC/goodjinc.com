---
title: "윈도우 11 마우스 우클릭 메뉴 이전 스타일로 되돌리기 (클래식 컨텍스트 메뉴)"
slug: "windows-11-classic-context-menu"
date: 2026-01-10T22:10:00+09:00
description: "Windows 11의 번거로운 '더 많은 옵션 표시' 메뉴를 제거하고, 윈도우 10 스타일의 클래식 우클릭 메뉴로 복구하는 가장 쉬운 방법을 안내합니다."
summary: "클릭 한 번으로 윈도우 11의 우클릭 메뉴를 이전 스타일로 되돌려 보세요. CMD 명령어와 레지스트리 파일을 모두 제공합니다."
categories: ["Tech"]
tags: ["Windows 11", "OS 설정", "생산성", "레지스트리"]
draft: false
# Thumbnail : https://pixabay.com/photos/digital-marketing-technology-1433427/
---

윈도우 11(Windows 11)의 새로운 컨텍스트 메뉴는 깔끔하긴 하지만, 매번 **더 많은 옵션 표시**를 클릭해야 하는 번거로움이 있습니다.

제가 Windows 11을 사용하면서 가장 먼저 느끼는 불편함은 아마도 마우스 우클릭 메뉴일 것입니다. 자주 사용하는 메뉴가 숨겨져있거나, 이전 윈도우 버전에서 사용하던 기본 단축키들을 사용하지 못할 때도 있습니다.

그래서 이번 시간에는 **레지스트리 수정**만으로 빠르게 윈도우 10(Windows 10) 스타일의 컨텍스트 메뉴로 설정하거나 복원하는 방법을 소개합니다.

---

## 1. 레지스트리 파일로 간편하게 설정하기

명령어 입력이 낯설거나 간편한 적용을 원하시는 분들을 위해 `원클릭 설정 파일`을 준비했습니다. 우선 어떤 코드로 구성되어 있는지 소개합니다.

### ① 이전 스타일로 적용하기

이전 버전(Windows 10)에서 사용하던 마우스 오른쪽 클릭 메뉴 스타일로 설정하는 레지스트리 코드입니다.

파일 다운로드 후 더블클릭하여 파일을 실행한 뒤 3. 변경 사항 즉시 반영하기 (탐색기 재시작) 단계를 따라 Windows 탐색기를 재시작해야 적용됩니다.

**소스 코드**:

```reg
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}]
@=""

[HKEY_CURRENT_USER\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32]
@=""
```

**파일 다운로드**:

- <a href="Enable-Classic-Context-Menu.reg" download="Enable-Classic-Context-Menu.reg" class="btn btn-primary" style="text-decoration: none; display: inline-block;">
    클래식 메뉴 적용 파일 다운로드
  </a>

> [!TIP] **파일 실행 후 할 행동**
> 파일 다운로드 및 실행 후 [3. 변경 사항 즉시 반영하기 (탐색기 재시작)](#restart-explorer) 단계를 따라 Windows 탐색기를 재시작해주세요.

### ② Windows 11 기본 스타일로 되돌리기

윈도우 11 설치 시 기본 적용되는 컨텍스트 메뉴 스타일로 되돌리는 레지스트리 코드입니다.

파일 다운로드 후 더블클릭하여 파일을 실행하면 기본 윈도우 11 스타일로 되돌아옵니다.

**소스 코드**:

```reg
Windows Registry Editor Version 5.00

[-HKEY_CURRENT_USER\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}]
```

**파일 다운로드**:

- <a href="Restore-Windows11-Context-Menu.reg" download="Restore-Windows11-Context-Menu.reg" class="btn btn-primary" style="text-decoration: none; display: inline-block;">
    윈도우 11 기본 메뉴 적용 파일 다운로드
  </a>

---

## 2. 명령 프롬프트(CMD)로 직접 설정하기

파일 다운로드가 찜찜하고 걱정이 된다면, CMD(명령 프롬프트)에서 아래 명령어를 복사하여 직접 입력하셔도 동일한 효과를 볼 수 있습니다.

### ① CMD 실행하기

윈도우 실행 단축키(`Win + R`)를 누른 뒤 `CMD`라는 명령어를 입력하여 실행합니다.

### ② 클래식 스타일의 메뉴 적용하기

- 아래 명령어를 복사하여 입력한 뒤 Enter를 눌러 실행해줍니다.

```Bash
reg add "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32" /f /ve
```

> [!TIP] **파일 실행 후 할 행동**
> 파일 다운로드 및 실행 후 [3. 변경 사항 즉시 반영하기 (탐색기 재시작)](#restart-explorer) 단계를 따라 Windows 탐색기를 재시작해주세요.

### ③ Windows 11 기본 스타일로 되돌리기

- 아래 명령어를 복사하여 입력한 뒤 Enter를 눌러 실행한 뒤 결과를 바로 확인해봅니다.

```Bash
reg delete "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}" /f
```

---

## 3. 변경 사항 즉시 반영하기 (탐색기 재시작) {#restart-explorer}

레지스트리를 수정했다고 해서 바로 메뉴 스타일이 바뀌지는 않습니다. 컴퓨터를 재부팅하거나, 아래 명령어로 **윈도우 탐색기(Explorer)** 를 재시작해야 합니다.

① `Ctrl + Shift + Esc`를 눌러 `작업 관리자`를 엽니다.

② `Windows 탐색기` 프로세스를 찾아 마우스 우클릭 후 **[다시 시작]** 을 클릭합니다.

③ 또는 `CMD`에 아래 명령어를 입력하여 실행합니다.

```Bash
taskkill /f /im explorer.exe & start explorer.exe
```

## 마치며

마이크로소프트(Microsoft)가 Windows 10의 공식 지원을 종료하고 Windows 11을 사용해야만 하는 입장에서 새로운 스타일에 적응해보려고 했습니다.

하지만 클릭 수가 늘어나고, 다른 소프트웨어와의 호환성이 떨어지거나 단축키가 다른 점 등 불편한 점이 너무 많았습니다.

필요에 따라 언제든지 원래 상태로 되돌리수도 있으니 부담없이 적용해보셔도 됩니다.
