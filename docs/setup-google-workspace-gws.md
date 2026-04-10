# Google Workspace gws CLI Setup Guide

這份文件用來協助需要使用 `Claude Code` TUI 的同仁，在 macOS 或 Windows 上安裝 Google Workspace 官方團隊維護的 `gws` CLI。

完成後，你可以在 `Claude Code` TUI 裡使用 Google Workspace 工具，例如：

- Google Drive
- Gmail
- Calendar
- Sheets
- Docs

這份文件不處理 `Claude Desktop` 的 MCP 整合。就目前這個 repo 的標準路線來說，`gws` 不是直接給 Claude Desktop 用的方案。

## 這份 setup 的目的

對公司同仁來說，Google Workspace 是共通工作環境。

如果你已經在用 `Claude Code` TUI，裝好 `gws` 之後，agent 可以在權限範圍內幫你做更多事，例如：

- 找 Google Drive 文件
- 讀 Gmail thread
- 讀 Calendar 行程
- 協助把 Google Workspace 裡的內容回收到本地知識庫

## 先確認你是否真的需要裝 `gws`

建議符合以下條件再安裝：

- 你平常會使用 `Claude Code` TUI，而不是只用 Claude Desktop GUI
- 你真的需要讀取 Gmail、Drive、Calendar 或其他 Google Workspace 資料
- 你已向雲端服務管理者申請 GCP OAuth Client 憑證

如果你只是需要本機 repo 操作，或只用 Claude Desktop GUI，通常不需要先裝 `gws`。

## 官方前提

依 `googleworkspace/cli` 官方說明：

- 需要 Node.js 18+ 才能用 `npm install`
- 也可以直接用 GitHub Releases 的預編譯 binary
- macOS 也可使用 Homebrew：`brew install googleworkspace-cli`
- OAuth 需要 Google Cloud project 與對應 credentials

在這個 repo 的標準安裝順序裡，建議先確認：

- [setup-nodejs.md](setup-nodejs.md)
- [setup-claude-code-cli.md](setup-claude-code-cli.md)

如果你在 Mac 想把 Homebrew 當成備用安裝方式，也可以先看：

- [setup-homebrew.md](setup-homebrew.md)

## 公司標準做法

對公司同仁，建議把 `gws` 設定收斂成單一路徑：

1. 向雲端服務管理者申請 GCP OAuth Client 憑證
2. 取得公司提供的 `client_secret.json`
3. 將檔案放在 `~/.config/gws/client_secret.json`
   Windows 對應 `%USERPROFILE%\\.config\\gws\\client_secret.json`
4. 執行 `gws auth login`
5. 之後以 `gws auth status` 驗證登入狀態

除非有明確 troubleshooting 需求，否則不要額外設定：

- `GOOGLE_WORKSPACE_CLI_CLIENT_ID`
- `GOOGLE_WORKSPACE_CLI_CLIENT_SECRET`
- `GOOGLE_OAUTH_CREDENTIALS`
- `GOOGLE_WORKSPACE_CLI_CREDENTIALS_FILE`

也不要把 `gcloud auth application-default login` 當作 `gws` 的必要安裝步驟。

原因是：如果同一台電腦同時存在 `gws` 自己的 OAuth 設定、shell 環境變數，以及 `gcloud` 的 Application Default Credentials（ADC），實際 API request 可能會受到舊的 Google Cloud 設定影響，導致 `gws auth status` 顯示的 project 跟錯誤訊息要求你 enable 的 project 不一致。

## 先決定你要走哪條登入路線

### 路線 A：公司已提供 OAuth client

這是目前最適合團隊 rollout 的方式。

你只需要：

1. 安裝 `gws`
2. 向雲端服務管理者申請 GCP OAuth Client 憑證
3. 把公司提供的 OAuth client JSON 放到指定位置
4. 執行 `gws auth login`
5. 在瀏覽器登入你的公司帳號

這裡提到的 GCP OAuth Client 憑證，實際上通常會以 `client_secret.json` 形式提供。

### 路線 B：自己建立 OAuth 設定

這只適合維運者、管理者或 PoC 情境。

你需要：

1. 有 Google Cloud project
2. 設定 OAuth consent screen
3. 建立 Desktop app client
4. 下載 `client_secret.json`
5. 執行 `gws auth login`

如果你只是一般同仁，請不要自己建立 OAuth client，先向雲端服務管理者申請。

對 FLH 同仁來說，預設應走 **路線 A**。

如果公司已提供 OAuth client，請不要把 `gws auth setup` 當作一般安裝步驟。`gws auth setup` 比較適合維運者或管理者用來初始化 Google Cloud project / OAuth 設定，不適合每位同仁各自執行。

## Step By Step 安裝

### 0. 打開 Terminal / PowerShell

- Mac：先讀 [mac-terminal-basics.md](mac-terminal-basics.md)
- Windows：先讀 [windows-terminal-basics.md](windows-terminal-basics.md)

### 1. 檢查是否已安裝

執行：

```bash
gws --version
```

如果有顯示版本號，代表已安裝，可以跳到「登入」。

如果看到 `command not found` 或「無法辨識」，繼續下一步。

### 2. macOS：安裝 gws CLI

這個 repo 的建議主線是優先用 `npm` 安裝，因為 `brew` 在這裡是 optional 工具，不是必要前提。

先執行：

```bash
npm install -g @googleworkspace/cli
```

安裝後再檢查一次：

```bash
gws --version
```

如果你的 Mac 已經有 Homebrew，而且你偏好用 Homebrew 管理 CLI，也可以改用：

```bash
brew install googleworkspace-cli
```

如果你的電腦還沒有 Homebrew，先看：

- [setup-homebrew.md](setup-homebrew.md)

### 2. Windows：安裝 gws CLI

Windows 上建議用 npm 安裝：

```powershell
npm install -g @googleworkspace/cli
```

安裝後再檢查一次：

```powershell
gws --version
```

如果 `npm` 不可用，先確認 Node.js 是否安裝完成：

```powershell
node --version
npm --version
```

如果沒有版本號，先看：

- [setup-nodejs.md](setup-nodejs.md)

## Step By Step 登入

### 路線 A：公司已提供 OAuth client

1. 向雲端服務管理者取得 GCP OAuth Client 憑證，也就是公司提供的 `client_secret.json`
2. 建立設定資料夾：

   **macOS（Terminal）：**

   ```bash
   mkdir -p ~/.config/gws
   ```

   **Windows（PowerShell）：**

   ```powershell
   New-Item -ItemType Directory -Path "$env:USERPROFILE\.config\gws" -Force
   ```

3. 把 `client_secret.json` 放到：

   - macOS：`~/.config/gws/client_secret.json`
   - Windows：`%USERPROFILE%\.config\gws\client_secret.json`

   **macOS Finder 方式**：
   1. 在 Finder 上方選單點 `Go` -> `Go to Folder...`，輸入 `~/.config/gws`，按 Enter
   2. 把公司提供的 JSON 檔拖進資料夾，並改名為 `client_secret.json`

   **Windows File Explorer 方式**：
   1. 在 File Explorer 地址列輸入 `%USERPROFILE%\.config\gws`，按 Enter
   2. 把公司提供的 JSON 檔拖進資料夾，並改名為 `client_secret.json`
   3. 若資料夾不存在，先執行上面的 PowerShell 指令建立

4. 確認檔案在正確位置：

   **macOS：**

   ```bash
   ls -l ~/.config/gws/client_secret.json
   ```

   **Windows：**

   ```powershell
   dir "$env:USERPROFILE\.config\gws\client_secret.json"
   ```

5. Windows 如遇到執行權限問題，先調整 PowerShell execution policy

   有些 Windows 電腦在執行 `gws auth login` 前，會先卡在 PowerShell 的執行權限。

   如果你遇到這種情況，請先用系統管理員身份開啟 PowerShell：

   1. 按 `Windows 鍵`
   2. 搜尋 `PowerShell`
   3. 看到 `Windows PowerShell` 後，不要直接點開
   4. 對它按右鍵，選擇「以系統管理員身份執行」
   5. 如果出現確認視窗，按「是」

   開啟後，執行：

   ```powershell
   Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
   ```

   完成後，再回來重新執行 `gws auth login`。

6. 執行登入：

   ```bash
   gws auth login
   ```

7. 瀏覽器會開啟登入頁面，請使用你的公司 Google 帳號登入
8. 完成授權後，回到 Terminal / PowerShell

### 路線 B：自己建立 OAuth client

如果你是維運者，或公司還沒有提供共用 OAuth client，請先完成這些步驟：

1. 到 Google Cloud Console 建立或選擇 project
2. 開啟 OAuth consent screen
3. App type 選 `External`
4. 把你自己的公司帳號加到 `Test users`
5. 建立一個 `Desktop app` OAuth client
6. 下載 JSON
7. 建立設定資料夾（macOS / Windows 分別見路線 A 步驟 2）
8. 把下載的 JSON 存到 `client_secret.json`（路徑見路線 A 步驟 3）
9. 確認位置正確後，執行：

```bash
gws auth login
```

如果你看到 `Access blocked`，通常是因為你沒有被加到 Test users。

## 驗證 gws 是否能正常使用

登入後，先做 preflight：

```bash
gws auth status
```

請至少確認：

- `client_config_exists: true`
- `token_valid: true`
- `user` 是你的公司帳號
- `project_id` 是公司指定 project

目前公司標準安裝預期的 `project_id` 應為：

```text
gen-lang-client-0301108841
```

確認 status 正常後，再跑一個最小測試：

```bash
gws drive files list --params '{"pageSize": 3}'
```

如果有回傳 JSON 結果，代表 `gws` 已經可以工作。

如果你目前只需要 Gmail，也可以請 agent 幫你用比較小範圍的 scope 重新登入。

## 如果錯誤訊息指向一個你沒設定過的 project

如果你看到類似下面這種錯誤：

```text
Google Drive API has not been used in project <some-other-project> before or it is disabled
```

而 `<some-other-project>` 不是你在 `client_secret.json` 或 `gws auth status` 看到的 project，通常代表這台電腦還有其他 Google 認證設定正在影響 `gws`。

建議依序檢查：

1. `gws auth status`
2. shell / PowerShell 是否有額外的 `GOOGLE_*` 或 `GWS_*` 環境變數
3. 是否存在舊的 `gcloud` ADC 設定

**macOS：**

```bash
gws auth status
env | rg '^GOOGLE|^GWS'
cat ~/.config/gcloud/application_default_credentials.json
```

**Windows（PowerShell）：**

```powershell
gws auth status
Get-ChildItem Env: | Where-Object { $_.Name -match '^(GOOGLE|GWS)' }
Get-Content "$env:APPDATA\gcloud\application_default_credentials.json"
```

如果 `application_default_credentials.json` 內出現：

```json
"quota_project_id": "某個不是公司標準的 project"
```

代表這台電腦上的 `gcloud` ADC 可能正在干擾 `gws` request routing / quota project。

### 建議修復順序

如果你不需要在這台電腦上保留 `gcloud` ADC，建議先清掉它，再重新做 `gws` 登入：

```bash
gcloud auth application-default revoke
gws auth logout
gws auth login
```

如果你需要保留 `gcloud`，但要讓它和公司標準 `gws` project 對齊，可改成：

```bash
gcloud auth application-default set-quota-project gen-lang-client-0301108841
```

做完後，再重新驗證：

```bash
gws auth status
gws drive files list --params '{"pageSize": 3}'
```

## 在 Claude Code TUI 內做最小驗收

完成登入後，可以在 `Claude Code` TUI 內測試問：

```text
請先確認我這台電腦上的 gws 是否可用，並列出我最近的 Google Drive 檔案。
```

或：

```text
請幫我整理今天 Gmail 最近幾封重要信件的重點。
```

如果 Claude Code 可以正常透過 `gws` 幫你執行查詢，代表這條路線大致可用。

## Agent-Assisted 安裝 Prompt

如果你已經有 Claude、Codex 或 Gemini 可以協助你，可以直接貼這段：

```text
我要在 Mac 上安裝 Google Workspace 的 gws CLI，並在 Claude Code TUI 裡使用。
我對 Terminal 不熟，請用繁體中文一步一步帶我做。

請遵守以下方式：
1. 每一步先叫我執行一個檢查或安裝指令
2. 等我貼出結果後，再告訴我下一步
3. 如果要修改設定檔，請先告訴我檔案路徑、再給我完整內容
4. 如果需要 OAuth 憑證，先提醒我向雲端服務管理者申請

我的驗收目標是：
- `gws --version` 成功
- `gws auth login` 完成
- `gws drive files list --params '{"pageSize": 3}'` 可用
- 我可以在 Claude Code TUI 裡問到 Drive 或 Gmail 資料
```

## 常見問題

### `gws: command not found`

代表尚未安裝完成，或 shell 沒有重新載入。先關掉 Terminal，再開一個新的視窗測試 `gws --version`。

### `Access blocked`

通常代表 OAuth consent screen 沒有把你加到 Test users，或公司提供的 OAuth client 還沒設定好。

### Windows 上出現執行權限或 script policy 問題

如果你在 Windows 執行 `gws auth login` 前後，遇到 PowerShell 執行權限相關錯誤，先用系統管理員身份開啟 PowerShell，然後執行：

```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```

做完後，重新開一個 PowerShell 視窗，再試一次 `gws auth login`。

### Claude Code 裡無法使用 Google Workspace

先檢查三件事：

1. `gws auth status` 是否正常
2. `gws` 指令在 Terminal / PowerShell 是否能正常執行
3. `client_secret.json` 是否放在正確位置

如果你還是不確定問題在哪裡，回頭先看：

- [workstation-final-check.md](workstation-final-check.md)
