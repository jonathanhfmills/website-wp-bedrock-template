<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-05-09 | Updated: 2026-05-09 -->

# sessions

## Purpose
此目錄乃各工作階段狀態之庫藏。每一子目錄以 UUID 命名，對應一次 OMC 工作階段，內藏 HUD 狀態及階段生命週期事件之紀錄。悉由工具自動生成，不可人力手改。

## Subdirectories
| Directory | Purpose |
|-----------|---------|
| `{uuid}/` | 各工作階段之狀態快照，含 `hud-state.json`（HUD 顯示狀態）及 `session-started.json`（階段啟動事件）；以 UUID 命名，由 OMC 自動建立 |

## For AI Agents

### Working In This Directory
此目錄之下，不得直接置入任何檔案；所有內容皆歸於以 UUID 命名之子目錄，每目錄對應一工作階段。子目錄內諸檔由 OMC 工具自動寫入，代理只可讀取，不可手動修改或新增。若需查閱當前 HUD 狀態，可讀對應階段目錄下之 `hud-state.json`；若需知階段啟動資訊，可覽 `session-started.json`。違規手改者，恐致 HUD 錯亂、階段狀態失序，編排層將無法正確追蹤任務進程。

<!-- MANUAL -->
