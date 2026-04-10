# Google Sheets MCP Setup Guide

這份文件用來協助主要使用 `Claude Desktop` GUI 的同仁，設定 Google Sheets MCP，讓 Claude 可以直接讀寫指定的 Google Sheets 檔案。

這條路線適合：

- 你主要在 Claude Desktop GUI 裡工作
- 你需要對少量固定的 Google Sheets 做可靠 read / write
- 你需要 cell 或 range 級別的更新，不只是新增一列
- 你可以接受用 Google Cloud service account 來做認證

這條路線不等於整個 Google Workspace 整合。如果你要在 `Claude Code` TUI 中使用 Gmail、Drive、Calendar 等工具，請改看：

- [setup-google-workspace-gws.md](setup-google-workspace-gws.md)

## 這份 setup 的核心做法

這個方案使用 `freema/mcp-gsheets` 作為本機直連的 Google Sheets MCP server。

你需要準備：

1. Node.js 18+
2. 一個已啟用 Google Sheets API 的 Google Cloud project
3. 一個 service account JSON key
4. 把你要操作的 Google Sheets 分享給該 service account email
5. 在 Claude Desktop 的 `claude_desktop_config.json` 中加入 `npx` 啟動設定

## 先確認你是否真的需要裝這個

建議符合以下條件再安裝：

- 你主要用 Claude Desktop，而不是只用 Claude Code CLI
- 你要直接修改 Google Sheets 內容
- 你可以向雲端服務管理者申請 service account JSON key，或由維運者代為建立

如果你只是要在本機整理 Markdown 或 repo，通常不需要這條。

## 官方前提

這個方案需要：

- Node.js 18 或更高版本
- `npm`
- Google Cloud project，並啟用 Google Sheets API
- service account JSON key

先完成這些基礎安裝：

- [setup-nodejs.md](setup-nodejs.md)
- [setup-claude-desktop-app.md](setup-claude-desktop-app.md)

## 公司標準做法

對公司同仁，建議把這條路線收斂成單一路徑：

1. 向雲端服務管理者申請 service account JSON key
2. 確認對方已在 GCP project 啟用 Google Sheets API
3. 把要操作的 Google Sheets 分享給 service account email
4. 把 key 檔存到本機固定路徑
5. 在 Claude Desktop 設定檔加入 `mcp-gsheets`

## Step By Step 設定

### 0. 打開 Terminal / PowerShell

- Mac：先讀 [mac-terminal-basics.md](mac-terminal-basics.md)
- Windows：先讀 [windows-terminal-basics.md](windows-terminal-basics.md)

### 1. 檢查 Node.js 是否可用

執行：

```bash
node --version
npm --version
```

如果沒有版本號，先回：

- [setup-nodejs.md](setup-nodejs.md)

### 2. 取得 service account JSON key

請向雲端服務管理者申請 service account JSON key。

你至少需要知道兩件事：

- key 檔放在哪裡
- service account email 是什麼

如果你是維運者，則需要自己完成：

1. 建立或選擇 Google Cloud project
2. 啟用 Google Sheets API
3. 建立 service account
4. 下載 JSON key

### 3. 把目標試算表分享給 service account

打開你要讓 Claude 操作的 Google Sheets。

按右上角 `Share`，把 service account email 加進去，並給它 `Editor` 權限。

如果沒有這一步，Claude Desktop 連上 MCP 後仍然可能會出現 permission denied。

### 4. 決定 key 檔路徑

建議放在容易管理、且不會亂移動的位置。

例如：

- macOS：`~/.config/mcp-gsheets/service-account-key.json`
- Windows：`%USERPROFILE%\.config\mcp-gsheets\service-account-key.json`

先建立資料夾：

**macOS：**

```bash
mkdir -p ~/.config/mcp-gsheets
```

**Windows：**

```powershell
New-Item -ItemType Directory -Path "$env:USERPROFILE\.config\mcp-gsheets" -Force
```

再把 JSON key 放進去。

### 5. 找到 Claude Desktop 設定檔

設定檔路徑：

- macOS：`~/Library/Application Support/Claude/claude_desktop_config.json`
- Windows：`%APPDATA%\Claude\claude_desktop_config.json`

如果你不知道怎麼打開或建立，先看：

- Mac：[edit-claude-desktop-config.md](edit-claude-desktop-config.md)
- Windows：[edit-claude-desktop-config-windows.md](edit-claude-desktop-config-windows.md)

### 6. 把 Google Sheets MCP server 加進設定檔

**macOS 範例：**

```json
{
  "mcpServers": {
    "mcp-gsheets": {
      "command": "npx",
      "args": ["-y", "mcp-gsheets@latest"],
      "env": {
        "GOOGLE_PROJECT_ID": "your-project-id",
        "GOOGLE_APPLICATION_CREDENTIALS": "/Users/your-name/.config/mcp-gsheets/service-account-key.json"
      }
    }
  }
}
```

**Windows 範例：**

```json
{
  "mcpServers": {
    "mcp-gsheets": {
      "command": "npx",
      "args": ["-y", "mcp-gsheets@latest"],
      "env": {
        "GOOGLE_PROJECT_ID": "your-project-id",
        "GOOGLE_APPLICATION_CREDENTIALS": "C:\\Users\\your-name\\.config\\mcp-gsheets\\service-account-key.json"
      }
    }
  }
}
```

注意：

- `GOOGLE_APPLICATION_CREDENTIALS` 要填 absolute path
- `GOOGLE_PROJECT_ID` 要填建立 service account 的 GCP project id
- 如果你本來就有別的 MCP server，不要覆蓋整份檔案，要把 `mcp-gsheets` 加進同一個 `mcpServers` 物件

### 7. 完全關閉再重開 Claude Desktop

修改設定檔後，請完整退出 Claude Desktop，再重新打開。

只關視窗通常不夠。

## 最小驗收

在 Claude Desktop 測試問：

```text
請先確認你能不能讀取這份 Google Sheets，並列出第一個工作表的欄位名稱。
```

或：

```text
請把這份試算表某個指定 range 更新成我接下來提供的內容，但先告訴我你準備修改哪個範圍。
```

如果 Claude 可以正常讀取、更新或 append 你分享過的試算表，代表這條路線大致可用。

## 這條方案適合什麼

- 直接讀取指定 spreadsheet 的 metadata 或 range
- 更新某個 cell / range
- append 新資料列
- 新增或刪除 sheet
- 做基本格式化、條件格式、chart 等操作

## 常見問題

### `npx` 找不到

先檢查：

```bash
npx --version
```

如果失敗，先回：

- [setup-nodejs.md](setup-nodejs.md)

### `Permission denied`

通常代表目標 Google Sheets 還沒分享給 service account email，或分享權限不夠。

先確認：

1. 你分享的是正確的 spreadsheet
2. 分享對象是 service account email，不是你自己的一般 Google 帳號
3. 權限至少是 `Editor`

### `Authentication failed`

通常代表：

- `GOOGLE_APPLICATION_CREDENTIALS` 路徑錯了
- JSON key 檔不存在
- `GOOGLE_PROJECT_ID` 不對
- GCP project 還沒啟用 Google Sheets API

### Claude Desktop 看不到工具

先依序檢查：

1. `claude_desktop_config.json` 路徑是否正確
2. JSON 格式是否正確
3. `npx` 在 Terminal / PowerShell 是否可用
4. Claude Desktop 是否有完整重開

## Agent-Assisted 安裝 Prompt

如果你想讓 Claude、Codex 或其他 agent 帶你設定，可以直接貼這段：

```text
我要在 Claude Desktop 加上 Google Sheets MCP，讓我可以直接讀寫指定的 Google Sheets。
我是非工程使用者，對 Terminal 不熟。

請用繁體中文一步一步帶我做，而且每一步都要：
1. 先叫我做一個檢查
2. 告訴我成功時會看到什麼
3. 告訴我失敗時代表什麼
4. 等我貼結果後，再帶我做下一步

請優先用 npx 的方式設定 `mcp-gsheets`。
如果需要 GCP service account 或 key 檔，先提醒我向雲端服務管理者申請。

目標是完成以下驗收：
- Claude Desktop 已加入 `mcp-gsheets`
- 目標 Google Sheets 已分享給 service account email
- Claude Desktop 可以讀取指定試算表
- Claude Desktop 可以更新指定 range
```
