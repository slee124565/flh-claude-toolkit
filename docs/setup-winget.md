# winget Setup Guide

這份文件說明 Windows 內建套件管理工具 `winget` 的基本用法。

`winget` 在 Windows 10（1709 以上）與 Windows 11 中已內建，不需要另外安裝。
它的角色類似 macOS 的 Homebrew，但在本指南中只用在少數工具，大多數工具仍建議直接用官方 installer。

## 先做什麼檢查

打開 PowerShell，執行：

```powershell
winget --version
```

如果有顯示版本號（例如 `v1.x.x`），代表這台 Windows 電腦已可使用 `winget`。

如果出現錯誤或「無法辨識」訊息，繼續往下看。

## 為什麼有時候需要 `winget`

本指南的多數工具都有獨立的官方 installer（例如 Git for Windows 與 Node.js），
直接下載安裝即可，不需要 `winget`。

但有些工具（例如 GitHub `gh` CLI）在 Windows 上使用 `winget` 安裝最為方便，
所以建議先確認 `winget` 可用。

## 如果 `winget` 不可用

### 情況 A：Windows 10 較舊版本

`winget` 需要 Windows 10 1709 或以上。先確認 Windows 版本：

1. 按 `Windows 鍵 + R`
2. 輸入 `winver`
3. 按 Enter，確認版本號是否符合

如果版本太舊，建議先更新 Windows，或透過 Microsoft Store 安裝「應用程式安裝程式」（App Installer）。

### 情況 B：版本符合但仍不可用

把完整錯誤訊息貼回 agent，請它帶你排查。

## 基本使用

安裝工具：

```powershell
winget install <工具名稱>
```

更新工具：

```powershell
winget upgrade <工具名稱>
```

例如，更新 Claude Code：

```powershell
winget upgrade Anthropic.ClaudeCode
```

## 在本指南中 `winget` 用在哪些地方

- `gh` CLI（選配）：[setup-github-gh-cli.md](setup-github-gh-cli.md)
- Claude Code CLI 的備用安裝方式：[setup-claude-code-cli.md](setup-claude-code-cli.md)

其餘工具（Git、Node.js、Claude Desktop App）都有獨立官方 installer，優先使用官方 installer。
