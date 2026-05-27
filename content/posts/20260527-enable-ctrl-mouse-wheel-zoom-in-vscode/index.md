---
title: "Visual Studio Code에서 Ctrl + 마우스 휠로 Font Size 조절 기능 활성화하기"
slug: "enable-ctrl-mouse-wheel-zoom-in-vscode"
date: 2026-05-27T13:00:00+09:00
description: "VS Code에서 코드 창의 글꼴 크기를 Ctrl + 마우스 휠 조작만으로 쉽고 빠르게 변경할 수 있도록 설정하는 방법을 알아봅니다."
summary: "비주얼 스튜디오 코드에서 매번 설정 창을 열지 않고, 키보드 Ctrl 키와 마우스 휠 동작만으로 폰트 크기를 실시간 조절하는 설정을 변경해 보세요."
categories: ["Development", "Editors"]
tags: ["VSCode", "Visual Studio Code", "Font Size", "Tip"]
draft: false
---

비주얼 스튜디오 코드(Visual Studio Code)를 사용할 때 화면 크기나 해상도에 따라 글꼴 크기(Font Size)를 빠르게 변경하고 싶을 때가 있습니다.

매번 설정 창(`Ctrl + ,`)을 열어 숫자를 직접 입력하는 방식은 꽤 번거롭습니다.

마우스 조작만으로 폰트를 확대 및 축소할 수 있도록 설정을 변경해 보겠습니다.

---

## 문제 원인 및 필요성

{{< figure src="img/vscode-font-zoom-problem.png" alt="VS Code에서 폰트 크기를 조절하기 위해 설정 창을 확인하는 모습" >}}

웹 브라우저나 다른 문서 편집기에서는 `Ctrl + 마우스 휠`을 굴리면 화면이 확대되거나 축소되는 기능이 기본적으로 활성화되어 있습니다.

하지만 VS Code의 기본 상태에서는 편집기 창의 폰트 크기가 마우스 휠 조작으로 변경되지 않도록 비활성화되어 있습니다. 

코딩 중 프레젠테이션을 하거나, 더 넓은 화면으로 코드를 한눈에 보고 싶을 때 이 기능을 켜두면 작업 효율을 크게 높일 수 있습니다.

---

## 문제 해결

1. `VSCode`에서 `Ctrl + ,`를 눌러 `설정`에 들어갑니다.

2. 검색창에 `Editor: Mouse Wheel Zoom`을 검색합니다.

3. 해당 옵션의 체크박스를 선택하여 `True`(활성화)로 변경합니다.

{{< figure src="img/vscode-mouse-wheel-zoom-setting-on.png" alt="VS Code 설정에서 Editor: Mouse Wheel Zoom 옵션을 체크하는 화면" >}}

4. 다시 작성 중인 코드로 돌아가서 `Ctrl` 키를 누른 채 마우스 휠을 위아래로 굴려 글꼴 크기가 실시간으로 변하는지 확인합니다.

{{< figure src="img/vscode-font-zoom-working.webp" alt="Ctrl + 마우스 휠 조작으로 글꼴 크기가 확대 및 축소되는 VS Code 편집기 화면" >}}
