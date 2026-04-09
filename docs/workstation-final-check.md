# Workstation Final Check

這份文件用來做整條工作站安裝主線的最後驗收。

如果你已經大致完成：

- Terminal 基本操作
- `git`
- Homebrew
- Node.js
- Claude Desktop App
- Claude Code CLI
- Google Workspace `gws`
- Claude Desktop MCP 設定

就用這份文件做一次總檢查。

## 最終目標

完成後，你應該可以：

- 在 Terminal 執行基本檢查指令
- 用 `git clone` 下載 public repo
- 在 Claude Desktop 正常對話
- 在 Terminal 正常啟動 `claude`
- 在 Claude Desktop 看到需要的 MCP 工具
- 讓 Claude 協助你讀本機 repo 或 Google Workspace 資料

## 第一組：CLI 是否就緒

請在 Terminal（Mac）或 PowerShell（Windows）逐條檢查：

**macOS：**

```bash
git --version
brew --version
node --version
npm --version
npx --version
claude --version
gws --version
```

**Windows：**

```powershell
git --version
winget --version
node --version
npm --version
npx --version
claude --version
gws --version
```

如果某個指令失敗，請回對應文件：

- `git`：
  [setup-git-cli.md](setup-git-cli.md)
- `brew`（macOS）：
  [setup-homebrew.md](setup-homebrew.md)
- `winget`（Windows）：
  [setup-winget.md](setup-winget.md)
- `node` / `npm` / `npx`：
  [setup-nodejs.md](setup-nodejs.md)
- `claude`：
  [setup-claude-code-cli.md](setup-claude-code-cli.md)
- `gws`：
  [setup-google-workspace-gws.md](setup-google-workspace-gws.md)

## 第二組：Claude Desktop 是否就緒

至少確認：

1. Claude Desktop App 可以正常打開
2. 你可以正常登入
3. 你可以進入對話畫面

如果這一步還沒完成，先回：

- [setup-claude-desktop-app.md](setup-claude-desktop-app.md)

## 第三組：Claude Code CLI 是否就緒

在 Terminal 執行：

```bash
claude doctor
```

如果可以正常跑出健康檢查結果，代表 `Claude Code CLI` 大致可用。

## 第四組：gws 是否已完成登入

在 Terminal 執行：

```bash
gws drive files list --params '{"pageSize": 3}'
```

如果有回傳結果，代表 `gws` 已經至少可正常讀取基本 Google Workspace 資料。

如果這一步失敗，先回：

- [setup-google-workspace-gws.md](setup-google-workspace-gws.md)

## 第五組：Claude Desktop MCP 設定是否就緒

先確認：

1. `claude_desktop_config.json` 已存在（路徑依 OS 不同）
2. 你要用的 server 已寫進 `mcpServers`
3. Claude Desktop 已完整退出再重開

設定檔路徑：

- macOS：`~/Library/Application Support/Claude/claude_desktop_config.json`
- Windows：`%APPDATA%\Claude\claude_desktop_config.json`

如果你不確定怎麼檢查或合併設定，先看：

- Mac：[edit-claude-desktop-config.md](edit-claude-desktop-config.md)
- Windows：[edit-claude-desktop-config-windows.md](edit-claude-desktop-config-windows.md)

## 第六組：最小工作流驗收

### 本機 repo 驗收

在 Claude Desktop 測試問：

```text
請檢查我目前這個 repo 的主要文件，並告訴我 README、CLAUDE、ARCHITECTURE 的分工。
```

如果 Claude 能正常回答，代表 `claude-code` MCP 路線大致可用。

### Google Workspace 驗收

如果你有接 `gws`，再測試問：

```text
請列出我最近的 Google Drive 檔案，並告訴我哪些值得我優先查看。
```

或：

```text
請幫我整理今天 Gmail 最近幾封重要信件的重點。
```

如果 Claude 能正常使用這些工具，代表 `gws` MCP 路線大致可用。

## 完成條件

你可以把這條主線視為完成，當以下條件都成立：

- `git --version` 成功
- `claude --version` 成功
- `claude doctor` 可用
- `gws --version` 成功
- `gws auth login` 已完成
- Claude Desktop 已加入需要的 MCP server
- Claude Desktop 可讀本機 repo 或 Google Workspace 資料

## 下一步

如果以上都完成，就可以前往：

- [llm-wiki-kb](https://github.com/slee124565/llm-wiki-kb/blob/main/README.md)

開始進入知識庫協作與內容整理。
