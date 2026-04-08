# flh-claude-toolkit

這是 FLH 內部的 Claude 工作站工具文件庫。

它的目的不是教你設計知識庫，而是幫你把一台 Mac 準備成公司同事可用的 Claude 工作環境，包含 GUI app、必要 CLI 工具與 MCP 整合。

## 你什麼時候該用這個 repo

當你遇到的是這類問題時，先來這裡：

- Terminal 還不熟
- 不確定 Mac 上有沒有 `git`
- 工具還沒裝好
- `command not found`
- Claude Desktop App 還沒裝好
- Claude Desktop 看不到本機工具
- MCP 還沒接好
- `gws`、`claude`、`gh` 不知道哪個是必要、哪個是選配

## 這個 repo 放什麼

- Terminal 基本操作
- Git CLI
- Homebrew
- Node.js
- Claude Desktop App
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

## 建議安裝主線

對多數公司同事，建議先完成這條標準路徑：

1. 熟悉 Terminal 基本操作
2. 確認 `git` CLI 可用
3. 安裝 Homebrew
4. 安裝 Node.js
5. 安裝 Claude Desktop App
6. 安裝 Claude Code CLI
7. 安裝 Google Workspace `gws`
8. 設定 terminal / MCP

`gh` CLI 不在這條主線裡。

如果你只是要 clone public GitHub repo，`git clone` 就夠用；只有在要做 private repo、PR、issue 或其他 GitHub 進階操作時，才需要再裝 `gh`。

## Repo 邊界

這個 repo 應聚焦在：

- 本機環境設定
- 安裝驗證
- 工具使用前置條件
- 故障排查與最小驗收
- 公司同事的標準工作站安裝順序

這個 repo 不應承接：

- 知識庫架構設計
- wiki 內容編排
- ingest / query / lint / maintenance 的知識庫工作流
