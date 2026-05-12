<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-05-09 | Updated: 2026-05-09 -->

# scripts

## Purpose
此目錄存容器初始化諸腳本。容器既建，`devcontainer.json` 之 `postCreateCommand` 調用 `init.sh` 為主入口，統御其餘腳本依序執行，完成環境配置之全程。

## Key Files
| File | Description |
|------|-------------|
| `init.sh` | 主入口腳本；容器啟動後首先執行，依序調用其餘諸腳本，統攬初始化全局 |
| `env-setup.sh` | 讀取環境變數範本，生成 `.env` 配置檔，為 WordPress Bedrock 提供運行所需之變量 |
| `git-credentials.sh` | 配置 Git 憑證助手，令容器內 Git 操作得以存取遠端倉庫而無需重複輸入密碼 |
| `git-workflow-setup.sh` | 設置 Git 鉤子與別名，規範提交流程，輔助開發者遵循專案工作流 |

## For AI Agents

### Working In This Directory
凡新增初始化邏輯，應擴充現有腳本或於 `init.sh` 內追加調用，切勿另立入口以亂執行順序。修改任一腳本後，須驗證 `init.sh` 整體流程仍可順利完成，各步驟之依賴關係不得打亂。腳本皆需具備冪等性，容器重建時可重複執行而無副作用。涉及密鑰或憑證者，應從環境變量或掛載之宿主機路徑取值，不可硬寫於腳本之中。

<!-- MANUAL -->
