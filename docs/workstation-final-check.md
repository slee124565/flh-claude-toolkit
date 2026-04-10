# Workstation Final Check

這份文件用來做整條工作站安裝主線的最後驗收。

如果你已經大致完成：

- Terminal 基本操作
- `git`
- Node.js
- Claude Desktop App

就用這份文件做一次總檢查。

## 最終目標

完成後，你應該可以：

- 在 Terminal 執行基本檢查指令
- 用 `git clone` 下載 public repo
- 在 Claude Desktop 正常對話
- 開始進入知識整理或文件協作流程

如果你另外有安裝進階工具，再額外驗收對應路線。

## 第一組：基礎 CLI 是否就緒

請在 Terminal（Mac）或 PowerShell（Windows）逐條檢查：

**macOS：**

```bash
git --version
node --version
npm --version
```

**Windows：**

```powershell
git --version
winget --version
node --version
npm --version
```

如果某個指令失敗，請回對應文件：

- `git`：
  [setup-git-cli.md](setup-git-cli.md)
- `winget`（Windows）：
  [setup-winget.md](setup-winget.md)
- `node` / `npm`：
  [setup-nodejs.md](setup-nodejs.md)

## 第二組：Claude Desktop 是否就緒

至少確認：

1. Claude Desktop App 可以正常打開
2. 你可以正常登入
3. 你可以進入對話畫面

如果這一步還沒完成，先回：

- [setup-claude-desktop-app.md](setup-claude-desktop-app.md)

## 第三組：基礎 GUI 工作流是否可用

在 Claude Desktop 測試問：

```text
請先用一句話告訴我你現在可以正常和我對話，然後再給我三個你可以協助我的簡單例子。
```

如果 Claude 能正常回答，代表基礎 GUI 工作流大致可用。

## 第四組：選配的 Claude Code CLI 是否就緒

如果你有安裝 `Claude Code CLI`，再檢查：

```bash
claude --version
claude doctor
```

如果你沒有安裝 `Claude Code CLI`，可以跳過這一組。

如果失敗，先回：

- [setup-claude-code-cli.md](setup-claude-code-cli.md)

## 第五組：選配的 Claude Desktop MCP 設定是否就緒

如果你有接任何 MCP server，再確認：

1. `claude_desktop_config.json` 已存在（路徑依 OS 不同）
2. 你要用的 server 已寫進 `mcpServers`
3. Claude Desktop 已完整退出再重開

設定檔路徑：

- macOS：`~/Library/Application Support/Claude/claude_desktop_config.json`
- Windows：`%APPDATA%\Claude\claude_desktop_config.json`

如果你目前沒有接任何 MCP server，可以跳過這一組。

如果你不確定怎麼檢查或合併設定，先看：

- Mac：[edit-claude-desktop-config.md](edit-claude-desktop-config.md)
- Windows：[edit-claude-desktop-config-windows.md](edit-claude-desktop-config-windows.md)

## 第六組：選配的 `gws` 是否已完成登入

如果你有安裝 `gws`，再執行：

```bash
gws drive files list --params '{"pageSize": 3}'
```

如果有回傳結果，代表 `gws` 已經至少可正常讀取基本 Google Workspace 資料。

如果你沒有要接 Google Workspace，可以跳過這一組。

如果失敗，先回：

- [setup-google-workspace-gws.md](setup-google-workspace-gws.md)

## 第七組：選配的 Google Sheets MCP 是否可用

如果你有接 Google Sheets MCP，可在 Claude Desktop 測試問：

```text
請先確認你能不能讀取我指定的 Google Sheets，然後告訴我第一個工作表目前有哪些欄位。
```

或：

```text
請幫我把這份試算表的某個 range 更新成我指定的新內容，但先告訴我你準備修改哪個範圍。
```

如果 Claude Desktop 能正常讀寫你分享給 service account 的試算表，代表 Google Sheets MCP 路線大致可用。

## 完成條件

你可以把這條主線視為完成，當以下條件都成立：

- `git --version` 成功
- `node --version` 成功
- `npm --version` 成功
- Claude Desktop 可以正常登入與對話

如果你有接 Claude Code CLI，再額外確認：

- `claude --version` 成功
- `claude doctor` 可用

如果你有接 Claude Desktop MCP，再額外確認：

- Claude Desktop 已加入需要的 MCP server
- Claude Desktop 可讀你預期暴露的工具

如果你有接 Google Workspace，再額外確認：

- `gws --version` 成功
- `gws auth login` 已完成
- `Claude Code` 可讀 Google Workspace 資料

如果你有接 Google Sheets MCP，再額外確認：

- Claude Desktop 已加入 Google Sheets MCP server
- 目標試算表已分享給 service account email
- Claude Desktop 可讀寫指定的 Google Sheets 資料

## 下一步

如果以上都完成，就可以前往：

- [llm-wiki-kb](https://github.com/slee124565/llm-wiki-kb/blob/main/README.md)

開始進入知識庫協作與內容整理。
