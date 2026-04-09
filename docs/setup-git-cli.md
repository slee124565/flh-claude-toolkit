# Git CLI Setup Guide

這份文件用來協助公司同事確認電腦上是否已具備 `git` CLI。

`git` 是本機版本控制與 clone public GitHub repo 的基礎工具。

如果你只是要把公開 repo 抓到本機，`git` 就夠了，不需要先安裝 GitHub `gh` CLI。

## 先做什麼檢查

打開 Terminal（Mac）或 PowerShell（Windows），執行：

```bash
git --version
```

如果有顯示版本號，代表這台電腦已可使用 `git`。

如果看到 `command not found` 或「無法辨識」，再照下面步驟處理。

## 為什麼先檢查 `git`

對這個 repo 的主要使用情境來說，`git` 最常用在兩件事：

- 讓本機資料夾具備版本控制能力
- 用 `git clone` 取得 public GitHub repo

`gh` 是進階 GitHub 操作工具，不是這兩件事的必要前提。

## Step By Step 安裝

### 1. 檢查是否已安裝

執行：

```bash
git --version
```

如果看到版本號，可以直接跳到後面的最小驗收。

### 2. macOS：如果系統跳出安裝視窗

有些 Mac 第一次執行 `git --version`，會跳出系統視窗，要求安裝 Apple Command Line Tools。

如果你看到這個視窗：

1. 按下安裝
2. 等待安裝完成
3. 完全關掉目前的 Terminal 視窗
4. 重新打開 Terminal
5. 再執行一次 `git --version`

### 2. Windows：安裝 Git for Windows

1. 用瀏覽器前往 Git for Windows 官方網站下載安裝檔
2. 執行 installer，安裝選項建議保持預設：
   - 勾選「Add Git to PATH」（確保 PowerShell 可以找到 git）
   - Git Bash 可選，不影響 PowerShell 使用
3. 安裝完成後，完全關掉 PowerShell
4. 重新打開 PowerShell
5. 執行：

```powershell
git --version
```

應該看到版本號。

### 3. 如果 `git` 仍不可用

先把完整錯誤訊息貼回 agent。

不要自己改 shell 設定或去下載不明來源的安裝包。

## 最小驗收

至少確認：

```bash
git --version
```

如果你接下來要把 `llm-wiki-kb` 抓到本機，也可以測試：

```bash
git clone https://github.com/slee124565/llm-wiki-kb.git
cd llm-wiki-kb
ls
```

你應該至少會看到：

- `raw`
- `wiki`
- `index.md`
- `log.md`

## 什麼時候才需要 `gh`

只有在你需要這些 GitHub 進階操作時，才建議再裝 `gh`：

- 存取 private repo
- 在本機看 PR / issue / repo 資訊
- 使用 `gh auth login` 做 GitHub 帳號登入

對應文件：

- [setup-github-gh-cli.md](setup-github-gh-cli.md)

## 常見問題

### `git --version` 跳出安裝視窗

這通常是正常的。

代表這台 Mac 還沒裝 Apple Command Line Tools，而 `git` 會跟著一起補上。

### `git: command not found`

先重新執行一次：

```bash
git --version
```

如果還是不行，把完整錯誤訊息貼回 agent。

### `git clone` 失敗

先把完整錯誤訊息貼回 agent。

常見原因包括：

- 網路問題
- repo URL 打錯
- 目標 repo 不是 public

## Agent-Assisted 安裝 Prompt

如果你想讓 Claude、Codex 或其他 agent 帶你確認 `git`，可以直接貼這段：

```text
請幫我確認這台 Mac 是否已可使用 git CLI。
我是非工程使用者，對 Terminal 不熟。

請用繁體中文一步一步帶我做，而且每一步都要：
1. 先叫我執行一個檢查
2. 告訴我成功時會看到什麼
3. 告訴我失敗時代表什麼
4. 等我貼結果後，再帶我做下一步

目標是完成以下驗收：
- `git --version` 成功
- 如果需要，macOS 的 Command Line Tools 安裝完成
- 我知道如何用 `git clone` 下載 public GitHub repo
```
