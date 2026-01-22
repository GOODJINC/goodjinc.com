---
title: "Visual Studio Code에서 한글 입력 시 노란색 박스 문제 해결하기"
slug: "resolve-yellow-box-typing-korean-in-vscode"
date: 2026-01-22T08:40:00+09:00
description: "VS Code에서 한글 입력 시 나타나는 신경 쓰이는 노란색 박스(유니코드 강조) 기능을 1분 만에 비활성화하여 가독성을 높이는 방법을 알아봅니다."
summary: "비주얼 스튜디오 코드에서 한글이 아스키 코드 외 문자로 인식되어 발생하는 노란색 하이라이트 현상, 설정 변경 하나로 깔끔하게 해결하세요."
categories: ["Development", "Editors"]
tags: ["VSCode", "Visual Studio Code", "Korean", "Tip"]
draft: false
---

비주얼 스튜디오 코드(Visual Studio Code)를 사용하다가 한글을 작성할 때 노란색 박스가 생긴다는 것을 알게 되었습니다.

그냥 무시하면서 사용했지만 너무나도 신경 쓰여서 결국 해결하기로 했습니다.

가독성이 떨어지기도 했고요.

---

## 문제 원인

{{< figure src="img/yellow-box-in-vscode.webp" alt="VS Code에서 한글에 노란색 박스가 생긴 모습" >}}

VSCode의 설정 중 기본 `아스키 코드(ASCII)외의 모든 문자`를 `강조`하여 표시하는 것이 기본값으로 설정되어 있습니다.

여기서 기본 아스키 코드란 U+0020부터 U+007E까지의 출력 가능한 문자를 말하는 것입니다.

한글은 아스키 코드를 초과하는 유니코드 문자에 포함되기 때문에 VS Code에서 노랑 박스가 설정되는 것입니다.

해당 기능이 활성화되어 있으면 보안이나 디버깅 상 좋다고는 하지만…

한글을 사용하는 입장에서는 불편해서 해결하려고 합니다.

---

## 문제 해결

1. `VSCode`에서 `Ctrl + ,`를 눌러 `설정`에 들어갑니다.

2. 검색창에 `Unicode Highlight: Non Basic ASCII`를 검색합니다.

```
Unicode Highlight: Non Basic ASCII

Controls whether all non-basic ASCII characters are highlighted.
Only characters between U+0020 and U+007E, tab, line-feed and carriage-return are considered basic ASCII.

유니코드 강조(하이라이트): 기본 아스키 코드 외

기본 ASCII 문자 외의 모든 문자를 강조 표시할지 여부를 제어합니다.
U+0020(스페이스)에서 U+007E(~) 사이의 문자, 탭, 줄 바꿈(Line Feed), 그리고 캐리지 리턴(Carriage Return)만 기본 ASCII 문자로 간주됩니다.
```

3. 해당 옵션을 `False`로 변경 및 설정합니다.

{{< figure src="img/vscode-unicode-highlight-setting-off.webp" alt="VS Code 설정에서 Unicode Highlight: Non Basic ASCII 옵션을 해제하는 화면" >}}

4. 다시 작성중인 코드로 돌아가서 해결되었는지 확인한다.

{{< figure src="img/vscode-korean-typing-fixed.webp" alt="노란색 박스 없이 한글이 정상적으로 표시되는 VS Code 편집기 화면" >}}
