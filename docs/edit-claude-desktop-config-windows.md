# Claude Desktop Config Editing Guide（Windows）

這份文件說明怎麼在 Windows 上找到、建立、修改 `Claude Desktop` 的 MCP 設定檔。

Mac 版請看：[edit-claude-desktop-config.md](edit-claude-desktop-config.md)

如果你前面看到其他文件寫：

- `%APPDATA%\Claude\claude_desktop_config.json`
- 把某段 JSON 加到 `mcpServers`

但你不知道要怎麼實際操作，就先看這份。

## 這份文件處理什麼問題

- 不知道 `claude_desktop_config.json` 在 Windows 的哪裡
- 不知道怎麼打開 `%APPDATA%` 路徑
- 檔案不存在，不知道怎麼建立
- 已經有別的 MCP server，不知道怎麼合併
- 改完後 Claude Desktop 還是看不到工具

## 設定檔路徑

Windows 路徑是：

```text
%APPDATA%\Claude\claude_desktop_config.json
```

`%APPDATA%` 是 Windows 的系統變數，實際上指向類似這樣的路徑：

```text
C:\Users\你的帳號\AppData\Roaming
```

不需要記完整路徑，直接用下方的方式打開就好。

## 方式 1：用 File Explorer 打開

如果你不熟 PowerShell，建議優先用這種方式。

1. 打開 File Explorer（資料夾圖示，或按 `Windows 鍵 + E`）
2. 點上方地址列，清空後輸入：

```text
%APPDATA%\Claude
```

3. 按 Enter
4. 找 `claude_desktop_config.json`

如果你有看到這個檔案，代表設定檔已存在。

如果你沒有看到這個檔案，也沒關係，代表你需要建立新檔。

## 方式 2：用 PowerShell 打開資料夾

如果你已經會執行一兩行指令，也可以用：

```powershell
explorer "$env:APPDATA\Claude"
```

這會直接在 File Explorer 打開對應資料夾。

## 如果資料夾不存在

第一次安裝 Claude Desktop App 後，`%APPDATA%\Claude` 資料夾可能還不存在。

用 PowerShell 建立資料夾：

```powershell
New-Item -ItemType Directory -Path "$env:APPDATA\Claude" -Force
```

執行後再用方式 1 打開確認。

## 如果檔案不存在，怎麼建立

建立資料夾後，用任一種方式建立設定檔：

- 在 File Explorer 裡建立一個新文字檔，再將副檔名改成 `.json`，命名為 `claude_desktop_config.json`
- 請 agent 給你完整 JSON，然後用記事本（Notepad）或 VS Code 貼上存檔

對非工程同仁，最穩的做法是：

1. 用記事本或 VS Code 打開新檔
2. 貼上 agent 給你的完整 JSON
3. 存到：

```text
%APPDATA%\Claude\claude_desktop_config.json
```

注意：存檔時確認副檔名是 `.json`，不是 `.json.txt`。

## 已有設定時，不要整份覆蓋

如果你已經有 `claude_desktop_config.json`，先打開檔案看目前內容。

常見情況有兩種。

### 情況 A：目前只有一個 MCP server

例如目前內容是：

```json
{
  "mcpServers": {
    "terminal": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-terminal"]
    }
  }
}
```

如果你要再加 `claude-code`，應改成：

```json
{
  "mcpServers": {
    "claude-code": {
      "type": "stdio",
      "command": "claude",
      "args": ["mcp", "serve"],
      "env": {}
    },
    "terminal": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-terminal"]
    }
  }
}
```

### 情況 B：目前已經有多個 server

不要重複寫第二個 `mcpServers`，把新 server 加進同一個 `mcpServers` 物件裡。

錯誤示意：

```json
{
  "mcpServers": {
    "terminal": {
      "command": "npx"
    }
  },
  "mcpServers": {
    "claude-code": {
      "command": "claude"
    }
  }
}
```

上面這種寫法是錯的，因為同一層不能有兩個 `mcpServers`。

## 改完後要做什麼

1. 存檔
2. 完全退出 Claude Desktop App（系統列右鍵 > 結束，或工作管理員確認關閉）
3. 再重新打開 Claude Desktop App

只關視窗通常不夠，請完整退出 App。

## 最小檢查清單

改完後，至少檢查：

1. JSON 看起來是完整的，最外層有一組 `{ }`
2. 只有一個 `mcpServers`
3. 每個 server 名稱都在 `mcpServers` 裡
4. Claude Desktop 已完整重開

## Claude Desktop 看不到工具時先檢查什麼

先依序檢查：

1. `claude_desktop_config.json` 有沒有存到正確路徑（`%APPDATA%\Claude\`）
2. JSON 格式有沒有壞掉
3. `command` 對應的 CLI 在 PowerShell 能不能執行
4. Claude Desktop App 是否真的有完整重開

如果 `command` 寫的是 `claude`、`npx`，可以在 PowerShell 測試：

```powershell
Get-Command claude
Get-Command npx
```

如果有任何一個找不到，就代表 Claude Desktop 也可能找不到。

## 相關文件

- 如果你要把 `Claude Code` 接進 Claude Desktop：
  [setup-terminal-mcp.md](setup-terminal-mcp.md)
- 如果你要在 Claude Desktop 使用 Google Sheets MCP：
  [setup-google-sheets-mcp.md](setup-google-sheets-mcp.md)
- 如果你要在 `Claude Code` TUI 使用 `gws`：
  [setup-google-workspace-gws.md](setup-google-workspace-gws.md)
- 如果你要做整條主線的最後驗收：
  [workstation-final-check.md](workstation-final-check.md)
