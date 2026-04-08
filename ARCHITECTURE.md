# ARCHITECTURE

這個 repo 的主題不是內容知識庫，而是 Claude 工作站設定與工具文件。

## Source-of-truth 分工

- `README.md`
  人類入口頁，說明 repo purpose、使用情境與和其他 repo 的分工
- `QUICKSTART.md`
  第一次使用者的線性 onboarding 路徑
- `docs/`
  穩定的安裝、設定、驗收、排查文件

## 內容邊界

這裡應收：

- local environment prerequisites
- CLI setup
- MCP setup
- troubleshooting
- 驗收與 quickstart 路徑

這裡不應收：

- wiki page 編排規則
- `raw/` / `wiki/` / `index.md` / `log.md` 的 operating model
- 特定知識庫的 ingest / query / lint / maintenance workflow

## 與 `llm-wiki-kb` 的關係

- 這個 repo 是 workstation layer
- `llm-wiki-kb` 是 knowledge base layer

兩者相關，但不應混成單一 repo。
