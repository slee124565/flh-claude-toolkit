# flh-claude-toolkit

這是 FLH 內部的 Claude 工作站工具文件庫。

它的目的不是教你設計知識庫，而是幫你把一台 Mac 準備成可與 Claude、CLI 工具與 MCP 協作的工作環境。

## 你什麼時候該用這個 repo

當你遇到的是這類問題時，先來這裡：

- Terminal 還不熟
- 工具還沒裝好
- `command not found`
- Claude Desktop 看不到本機工具
- MCP 還沒接好
- `gh`、`gws`、`claude` 不知道先裝哪個

## 這個 repo 放什麼

- Terminal 基本操作
- Homebrew
- Node.js
- GitHub `gh` CLI
- Claude Code CLI
- MCP 設定
- Google Workspace `gws` CLI / MCP
- 安裝驗收與 troubleshooting 文件

## 先從哪裡開始

如果你是第一次接觸這套工作流，先讀：

- [QUICKSTART.md](QUICKSTART.md)

如果你已經知道自己要裝什麼工具，直接看：

- [docs/README.md](docs/README.md)

## 和 `llm-wiki-kb` 的分工

- `flh-claude-toolkit`
  負責工作站設定、工具安裝、CLI、MCP 與 troubleshooting
- `llm-wiki-kb`
  負責知識庫結構、資料整理、索引與維護流程

順序是：

1. 先用 `flh-claude-toolkit` 把工作站設好
2. 再到 [`llm-wiki-kb`](https://github.com/slee124565/llm-wiki-kb/blob/main/README.md) 開始與 Claude 協作沉澱工作知識

## Repo 邊界

這個 repo 應聚焦在：

- 本機環境設定
- 安裝驗證
- 工具使用前置條件
- 故障排查與最小驗收

這個 repo 不應承接：

- 知識庫架構設計
- wiki 內容編排
- ingest / query / lint / maintenance 的知識庫工作流
