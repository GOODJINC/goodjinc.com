---
title: "How to Restore the Windows 11 Classic Context Menu (Right-Click Menu)"
slug: "windows-11-classic-context-menu"
date: 2026-01-10T22:10:00+09:00
description: "Remove the annoying 'Show more options' in Windows 11 and restore the classic Windows 10 style right-click menu with this simple guide."
summary: "Switch back to the classic Windows 11 context menu with a single click. We provide both CMD commands and ready-to-use Registry files."
categories: ["Tech"]
tags: ["Windows 11", "OS Settings", "Productivity", "Registry"]
draft: false
---

The new context menu in **Windows 11** looks sleek, but having to click **"Show more options"** every single time is a significant productivity killer.

One of the first frustrations many users face after upgrading to Windows 11 is this redesigned right-click menu. Frequently used commands are often hidden, and familiar keyboard shortcuts from previous Windows versions may no longer work as expected.

In this guide, I will show you how to quickly set or restore the **Windows 10 style context menu** using simple **Registry edits**.

---

## 1. Easy Setup Using Registry Files

For those who find manual commands intimidating or simply prefer a `one-click solution`, I have prepared ready-to-use Registry (.reg) files. Here is the code they contain:

### ① Apply Classic Style

This Registry code restores the familiar right-click menu style used in Windows 10.

**Source Code**:

```reg
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}]
@=""

[HKEY_CURRENT_USER\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32]
@=""
```

**Download File**:

- <a href="Enable-Classic-Context-Menu.reg" download="Enable-Classic-Context-Menu.reg" class="btn btn-primary" style="text-decoration: none; display: inline-block;">
    Download Classic Menu Fix
  </a>

> [!TIP] **Action Required After Execution:**
> After running the downloaded file, you must restart Windows Explorer to see the changes. Follow the steps in [3. Applying Changes (Restarting Explorer)](#restart-explorer).

### ② Restore Windows 11 Default Style

If you wish to revert to the default Windows 11 context menu style, use this code.

**Source Code**:

```reg
Windows Registry Editor Version 5.00

[-HKEY_CURRENT_USER\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}]
Download File:
```

**Download File**:

- <a href="Restore-Windows11-Context-Menu.reg" download="Restore-Windows11-Context-Menu.reg" class="btn btn-primary" style="text-decoration: none; display: inline-block;">
    Restore Default Windows 11 Menu
  </a>

---

## 2. Manual Setup via Command Prompt (CMD)

If you prefer not to download files, you can achieve the same result by entering commands directly into the Command Prompt (CMD).

### ① Launch CMD

Press `Win + R`, type `cmd`, and press Enter.

### ② Apply Classic Style Menu

Copy and paste the following command, then press Enter:

```Bash
reg add "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32" /f /ve
```

> [!TIP] **Note:**
> Don't forget to follow the [Restart Explorer step](#restart-explorer) below to apply the changes.

### ③ Revert to Windows 11 Default Style

To go back to the original Windows 11 style, run this command:

```Bash
reg delete "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}" /f
```

---

## 3. Applying Changes (Restarting Explorer) {#restart-explorer}

Registry edits do not take effect immediately. You must either restart your PC or manually restart Windows Explorer using the following steps:

① Press `Ctrl + Shift + Esc` to open the `Task Manager`.

② Locate the `Windows Explorer` process, right-click it, and select **[Restart]**.

③ Alternatively, you can run this command in your `CMD` window:

```Bash
taskkill /f /im explorer.exe & start explorer.exe
```

---

## Conclusion

As Microsoft ends official support for Windows 10, many of us are forced to transition to Windows 11.

While the new UI has its merits, the increased click count and compatibility issues with third-party software can be frustrating.

Since these changes are easily reversible, feel free to try the classic menu to see if it improves your workflow.
