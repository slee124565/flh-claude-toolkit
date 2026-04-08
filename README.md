# flh-claude-toolkit

一個給非工程同仁使用的 agent workstation onboarding starter。

這個 repo 不教你如何設計 wiki 架構本體，而是幫你先把一台 Mac 設成可與 agent 協作的本地工作環境。

它主要承接這類內容：

- Terminal 基本操作
- Homebrew
- Node.js
- GitHub `gh` CLI
- Claude Desktop App
- Claude Code CLI
- Claude skills / local agent workflow
- MCP server setup
- Google Workspace `gws` CLI / MCP

## 這個 Repo 用來做什麼

當你遇到的問題不是「wiki 要怎麼設計」，而是：

- 工具還沒裝好
- Terminal 不熟
- Claude Desktop 與本機環境怎麼配合不清楚
- MCP 怎麼接
- `gh`、`gws`、`claude` 該先裝什麼

這個 repo 就是環境設定與 onboarding 的入口。

## 與 `llm-wiki-kb` 的分工

- `flh-claude-toolkit`
  負責本機環境、工具安裝、MCP、CLI、troubleshooting、agent-assisted setup
- `llm-wiki-kb`
  負責知識庫 operating model、repo 結構、ingest / query / lint / maintenance workflow

簡單說：

- 先把工作站設好，再去經營 wiki

## 建議閱讀順序

1. `docs/mac-terminal-basics.md`
2. `docs/setup-homebrew.md`
3. `docs/setup-nodejs.md`
4. `docs/setup-github-gh-cli.md`
5. `docs/setup-claude-code-cli.md`
6. `docs/setup-terminal-mcp.md`
7. `docs/setup-google-workspace-gws.md`

## 當前狀態

目前這個 repo 已補到可發佈的最小完整狀態，但仍是 boundary refactor 的工作副本。

後續會視需要再從 `publishes/llm-wiki-kb` 完成剩餘導流收尾，讓兩個 repo 的主題邊界更乾淨。
