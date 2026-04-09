# Windows Terminal Basics

這份文件給第一次接觸 PowerShell 的 Windows 使用者。

目標不是讓你變成工程師，而是讓你能安全地完成三件事：

1. 打開 PowerShell
2. 貼上一行指令並執行
3. 把結果貼回 Claude 或其他 agent，讓它繼續帶你做

## 你會用到的觀念

- `PowerShell`
  Windows 內建的文字介面，可以執行指令
- `Command`
  你貼進去的一行文字，例如 `git --version`
- `Enter`
  貼完指令後按下去，電腦就會執行
- `Output`
  PowerShell 顯示的結果，用來判斷成功或失敗

## 第一次打開 PowerShell

1. 按 `Windows 鍵`
2. 輸入 `PowerShell`
3. 看到「Windows PowerShell」後按 Enter 打開

打開後你會看到一個可以輸入文字的畫面，提示符大致像這樣：

```text
PS C:\Users\你的帳號>
```

`PS C:\` 開頭代表你在 PowerShell 環境。

## 確認你在 PowerShell，而不是 CMD

Windows 有兩種文字介面：

- `PS C:\` 開頭 → PowerShell（本指南使用的環境）
- `C:\` 開頭 → 舊版命令提示字元（CMD）

本指南所有指令都以 PowerShell 為準。如果不確定，直接搜尋「Windows PowerShell」重新打開。

## 最基本操作

### 執行一行指令

1. 把指令完整複製
2. 在 PowerShell 視窗點一下
3. 貼上指令（Ctrl + V 或右鍵 > 貼上）
4. 按 Enter

### 看懂成功或失敗

通常有三種情況：

- 成功
  會看到版本號、清單、登入網址，或明確的 success 訊息
- 尚未安裝
  常見訊息像是 `command not found` 或「無法辨識 ... 命令」
- 權限或設定不完整
  會看到 `not authenticated`、`permission denied`、`access blocked` 之類訊息

只要把完整訊息貼回 Claude，agent 通常就能接著判斷下一步。

### 中止目前指令

如果畫面卡住或你執行錯了，可以按：

```text
Ctrl + C
```

## 這幾個檢查指令最常用

### 檢查工具有沒有裝好

```powershell
git --version
winget --version
node --version
npm --version
npx --version
claude --version
gws --version
gh --version
```

如果工具有問題，可以直接看這些對應文件：

- `git --version` 失敗：
  [setup-git-cli.md](setup-git-cli.md)
- `winget --version` 失敗：
  [setup-winget.md](setup-winget.md)
- `node --version`、`npm --version`、`npx --version` 失敗：
  [setup-nodejs.md](setup-nodejs.md)
- Claude Desktop App 還沒裝好或打不開：
  [setup-claude-desktop-app.md](setup-claude-desktop-app.md)
- `claude --version` 失敗：
  [setup-claude-code-cli.md](setup-claude-code-cli.md)
- `gws --version` 失敗：
  [setup-google-workspace-gws.md](setup-google-workspace-gws.md)
- `claude` 已安裝，但 Claude Desktop 裡的 terminal / MCP 能力還不能用：
  [setup-terminal-mcp.md](setup-terminal-mcp.md)
- `gh --version` 失敗：
  [setup-github-gh-cli.md](setup-github-gh-cli.md)

### 看目前在哪個資料夾

```powershell
pwd
```

### 看資料夾裡有哪些檔案

```powershell
ls
```

## 什麼時候要停下來問 agent

遇到以下情況，不要自己亂猜，直接把畫面貼回 Claude 或其他 agent：

- 看不懂 PowerShell 顯示什麼
- 指令跑很久沒有結束
- 跑出登入網址但不知道下一步
- 要你修改設定檔，不確定該貼什麼內容
- 出現紅字錯誤訊息

## 推薦用法

對非工程同仁，最穩的用法是：

1. 先請 agent 給你一個步驟
2. 只執行那一個步驟
3. 把結果貼回去
4. 再做下一步

這樣比一次貼一大串命令安全很多。
