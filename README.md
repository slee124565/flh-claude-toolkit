# flh-claude-toolkit

這是 FLH 內部給非工程同仁使用的 Claude 工作站入門工具包。

它的用途是先把一台 Mac 設成可與 Claude 和本機工具協作的環境，處理的是 setup，不是知識庫架構設計。

適合用在這些情境：

- Terminal 還不熟
- 工具還沒裝好
- `command not found`、登入失敗、MCP 設定不順
- 想用 Claude Desktop、Claude Code CLI、`gh`、`gws` 協助完成日常工作

## 這裡放什麼

- Terminal 基本操作
- Homebrew
- Node.js
- GitHub `gh` CLI
- Claude Desktop App
- Claude Code CLI
- MCP 設定
- Google Workspace `gws` CLI / MCP

## 先看哪裡

1. [docs/mac-terminal-basics.md](docs/mac-terminal-basics.md)
2. [docs/setup-homebrew.md](docs/setup-homebrew.md)
3. [docs/setup-nodejs.md](docs/setup-nodejs.md)
4. [docs/setup-github-gh-cli.md](docs/setup-github-gh-cli.md)
5. [docs/setup-claude-code-cli.md](docs/setup-claude-code-cli.md)
6. [docs/setup-terminal-mcp.md](docs/setup-terminal-mcp.md)
7. [docs/setup-google-workspace-gws.md](docs/setup-google-workspace-gws.md)

## 和 `llm-wiki-kb` 的分工

- `flh-claude-toolkit`
  負責工作站設定、工具安裝、MCP、CLI 與 troubleshooting
- `llm-wiki-kb`
  負責知識庫結構、資料整理、索引與維護流程

簡單說：

- 先把工作站設好，再去經營 wiki

## Repo 邊界

這個 repo 應該維持在：

- 本機環境設定
- 安裝驗證
- 使用前置條件
- 逐步排查

如果你要的是知識庫操作模式，請看：

- [llm-wiki-kb](../llm-wiki-kb/README.md)
