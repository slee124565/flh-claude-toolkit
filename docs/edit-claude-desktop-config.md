# Claude Desktop Config Editing Guide

這份文件專門說明怎麼在 Mac 上找到、建立、修改 `Claude Desktop` 的 MCP 設定檔。

如果你前面看到其他文件寫：

- `~/Library/Application Support/Claude/claude_desktop_config.json`
- 把某段 JSON 加到 `mcpServers`

但你不知道要怎麼實際操作，就先看這份。

## 這份文件處理什麼問題

它主要處理這些高頻卡點：

- 不知道 `claude_desktop_config.json` 在哪裡
- 不知道怎麼打開隱藏路徑
- 檔案不存在，不知道怎麼建立
- 已經有別的 MCP server，不知道怎麼合併
- 改完後 Claude Desktop 還是看不到工具

## 設定檔路徑

macOS 路徑是：

```text
~/Library/Application Support/Claude/claude_desktop_config.json
```

## 方式 1：用 Finder 打開

如果你不熟 Terminal，建議優先用這種方式。

1. 打開 Finder
2. 在上方選單點 `Go`
3. 點 `Go to Folder...`
4. 輸入：

```text
~/Library/Application Support/Claude
```

5. 按 Enter
6. 找 `claude_desktop_config.json`

如果你有看到這個檔案，就代表設定檔已存在。

如果你沒有看到這個檔案，也沒關係，代表你需要建立新檔。

## 方式 2：用 Terminal 打開資料夾

如果你已經會執行一兩行指令，也可以用：

```bash
open ~/Library/Application\ Support/Claude
```

這會直接在 Finder 打開對應資料夾。

## 如果檔案不存在，怎麼建立

你可以用任一種方式：

- 在 Finder 裡建立一個純文字檔，再命名成 `claude_desktop_config.json`
- 請 agent 給你完整 JSON，然後用文字編輯器貼上存檔

對非工程同仁，最穩的做法是：

1. 先用 `TextEdit` 或 `VS Code` 打開新檔
2. 貼上 agent 給你的完整 JSON
3. 存到：

```text
~/Library/Application Support/Claude/claude_desktop_config.json
```

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

這時不要重複寫第二個 `mcpServers`。

正確做法是把新 server 加進同一個 `mcpServers` 物件裡。

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
2. 完全退出 Claude Desktop App
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

1. `claude_desktop_config.json` 有沒有存對路徑
2. JSON 格式有沒有壞掉
3. `command` 對應的 CLI 在 Terminal 能不能執行
4. Claude Desktop App 是否真的有完整重開

如果 `command` 寫的是：

- `claude`
- `npx`

可以先在 Terminal 測試：

```bash
which claude
which npx
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
