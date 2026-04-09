# Claude Desktop App Setup Guide

這份文件用來協助公司同事先把 `Claude Desktop App` 裝好。

對非工程同仁來說，這通常是最自然的 Claude 使用入口。

後面的 `Claude Code CLI`、`gws` CLI 與 MCP 設定，都是在這個基礎上往外擴充能力。

## 先確認你為什麼要先裝這個

如果你的主要工作方式是：

- 在 GUI 裡和 Claude 對話
- 用 Claude Desktop 接公司工具
- 讓 Claude 之後可以看到本機或 Google Workspace 工具

那就應該先完成 Claude Desktop App。

## 先做什麼檢查

確認電腦上是否已安裝 Claude Desktop App：

- **macOS**：在 Spotlight 搜尋 `Claude`
- **Windows**：按 `Windows 鍵`，搜尋 `Claude`

如果已能正常打開並登入 Claude 帳號，可以先繼續後面的 CLI 與 MCP 文件。

## Step By Step 安裝

### 1. 下載 Claude Desktop App

請從 Anthropic 官方網站下載對應作業系統的安裝檔：

- **macOS**：下載 `.dmg` 或 `.pkg`
- **Windows**：下載 `.exe` installer

### 2. 安裝 App

**macOS**：依 macOS 一般 App 安裝方式完成安裝，並把 App 放到 `Applications`。

**Windows**：執行下載的 `.exe` installer，依畫面指示完成安裝。
安裝完成後，Claude Desktop App 會出現在開始選單。

### 3. 第一次啟動

打開 Claude Desktop App。

第一次啟動時，依畫面指示登入你的 Claude 帳號。

### 4. 最小驗收

至少確認：

- Claude Desktop App 可以正常打開
- 你可以完成登入
- 你可以進入對話畫面

## 裝好後下一步去哪裡

如果你接下來要：

- 補齊本機 repo 基礎能力：
  [setup-git-cli.md](setup-git-cli.md)
- 安裝 Claude Code CLI：
  [setup-claude-code-cli.md](setup-claude-code-cli.md)
- 安裝 Google Workspace `gws`：
  [setup-google-workspace-gws.md](setup-google-workspace-gws.md)
- 設定 Claude Desktop 裡的 terminal / MCP：
  [setup-terminal-mcp.md](setup-terminal-mcp.md)

## 常見問題

### 不知道自己有沒有裝過 Claude Desktop App

- macOS：用 Spotlight 搜尋 `Claude`
- Windows：按 `Windows 鍵` 搜尋 `Claude`

如果找不到，代表大概率尚未安裝。

### App 打得開，但不知道有沒有登入

只要重新打開後能直接進入 Claude 對話畫面，通常就代表已登入。

如果一直卡在登入畫面，請先完成登入再繼續後面的 setup。

### 想直接用 CLI，不想先裝 Desktop App

可以，但這不符合這個 repo 預設的公司同事主路徑。

這個 repo 預設先把 Claude Desktop App 當成主要 GUI 入口，再延伸到 CLI 與 MCP。

## Agent-Assisted 安裝 Prompt

如果你想讓 Claude、Codex 或其他 agent 陪你確認這一步，可以直接貼這段：

```text
請幫我確認這台電腦是否已裝好 Claude Desktop App，並帶我完成最小驗收。
我是非工程使用者，對 Terminal 不熟。

請用繁體中文一步一步帶我做，而且每一步都要：
1. 先叫我做一個檢查
2. 告訴我成功時會看到什麼
3. 告訴我失敗時代表什麼
4. 等我貼結果後，再帶我做下一步

目標是完成以下驗收：
- Claude Desktop App 已安裝
- 我可以正常登入
- 我知道下一步要接哪一份 setup 文件
```
