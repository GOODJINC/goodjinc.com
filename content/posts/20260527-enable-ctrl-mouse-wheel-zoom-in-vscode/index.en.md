---
title: "Enabling Font Size Adjustment with Ctrl + Mouse Wheel in Visual Studio Code"
slug: "enable-ctrl-mouse-wheel-zoom-in-vscode"
date: 2026-05-27T13:00:00+09:00
description: "Learn how to configure VS Code so you can quickly and easily change the editor font size using just Ctrl + Mouse Wheel."
summary: "Change your Visual Studio Code settings to adjust the font size in real time using the Ctrl key and mouse wheel, without having to open the settings menu every time."
categories: ["Development", "Editors"]
tags: ["VSCode", "Visual Studio Code", "Font Size", "Tip"]
draft: false
---

When using Visual Studio Code, you might want to quickly change the font size depending on your screen size or resolution.

Manually entering a number in the Settings window (`Ctrl + ,`) every time can be quite tedious.

Let's change the settings to zoom the font in and out using simple mouse controls.

---

## Why Enable This Feature?

{{< figure src="img/vscode-font-zoom-problem.png" alt="Checking the Settings menu in VS Code to adjust font size" >}}

In web browsers and other text editors, zooming in or out by scrolling the mouse wheel while holding `Ctrl` is typically enabled by default.

However, by default in VS Code, the editor font size zoom via mouse wheel is disabled.

Enabling this feature can greatly improve your workflow efficiency when presenting code or trying to fit more code on the screen at a glance.

---

## How to Enable It

1. Press `Ctrl + ,` in VS Code to open **Settings**.

2. Search for `Editor: Mouse Wheel Zoom` in the search bar.

3. Check the checkbox for the option to enable it (`true`).

{{< figure src="img/vscode-mouse-wheel-zoom-setting-on.png" alt="Checking the Editor: Mouse Wheel Zoom option in VS Code Settings" >}}

4. Return to your editor and scroll the mouse wheel up or down while holding down the `Ctrl` key to confirm that the font size changes in real time.

{{< figure src="img/vscode-font-zoom-working.png" alt="VS Code editor showing the font size zooming in and out with Ctrl + mouse wheel scroll" >}}
