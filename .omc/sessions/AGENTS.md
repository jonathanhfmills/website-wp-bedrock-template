<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-05-09 | Updated: 2026-05-09 -->

# sessions

## Purpose
此目錄存 OMC 工作階段之 JSON 狀態檔，每檔以 UUID 命名，對應一次會話。悉由 OMC 工具自動寫入，不可人力手改。

## Key Files
| File | Description |
|------|-------------|
| `{uuid}.json` | 單次工作階段之狀態快照，由 OMC 工具生成與維護 |

## For AI Agents

### Working In This Directory
此目錄之所有檔案皆由 OMC 工具自動管理，代理只可讀取，不可新增、修改或刪除。如需取用階段狀態，透過 OMC 工具介面存取，勿直接操作此目錄之 JSON 檔。

<!-- MANUAL -->
