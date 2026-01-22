---
title: "How to Fix the Yellow Box Issue When Typing Korean in VS Code"
slug: "resolve-yellow-box-typing-korean-in-vscode"
date: 2026-01-22T08:40:00+09:00
description: "Learn how to disable the distracting yellow boxes (Unicode highlighting) that appear when typing Korean in Visual Studio Code to improve readability."
summary: "Tired of the yellow highlights on Korean characters in VS Code? This occurs because they are recognized as non-basic ASCII. Here is a simple fix to clean up your editor."
categories: ["Development", "Editors"]
tags: ["VSCode", "Visual Studio Code", "Korean", "Tip", "Troubleshooting"]
draft: false
---

While using Visual Studio Code, I noticed that yellow boxes would appear around Korean characters as I typed.

I tried to ignore it at first, but it became too distracting and significantly reduced readability. I finally decided to fix it once and for all.

---

## The Cause

{{< figure src="img/yellow-box-in-vscode.webp" alt="Yellow boxes appearing on Korean text in VS Code" >}}

By default, VS Code has a setting enabled that highlights `all characters outside the basic ASCII range`.

The "basic ASCII" range refers to printable characters between U+0020 and U+007E. Since Korean characters are Unicode characters that fall outside this range, VS Code flags them with a yellow highlight.

While this feature is intended to be helpful for security (identifying invisible or confusing characters) and debugging, it is quite inconvenient for those of us who frequently type in Korean.

---

## The Solution

1. Open `Settings` in `VS Code` by pressing `Ctrl + ,`.

2. Search for `Unicode Highlight: Non Basic ASCII` in the search bar.

```text
Unicode Highlight: Non Basic ASCII

Controls whether all non-basic ASCII characters are highlighted.
Only characters between U+0020 and U+007E, tab, line-feed and carriage-return are considered basic ASCII.
```

3. Set this option to `False` (uncheck the box).

{{< figure src="img/vscode-unicode-highlight-setting-off.webp" alt="Disabling the 'Unicode Highlight: Non Basic ASCII' option in VS Code settings" >}}

4. Return to your code editor and verify that the yellow boxes are gone.

{{< figure src="img/vscode-korean-typing-fixed.webp" alt="VS Code editor screen showing Korean text without yellow highlights" >}}
