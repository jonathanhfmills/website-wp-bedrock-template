<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-05-09 | Updated: 2026-05-09 -->

# state

## Purpose
此目錄乃 OMC 編排層運行時之狀態儲所。凡當前任務之進程、衍生代理之名冊、HUD 顯示之快取，皆歸於此。此乃工具自治之域，非人力著筆之處，代理宜讀而慎改。

## Key Files
| File | Description |
|------|-------------|
| `mission-state.json` | 記錄當前活躍任務之狀態，乃編排層知悉任務進展之根本所在 |
| `subagent-tracking.json` | 已衍生之子代理名冊，記其身份、職司與存活之狀 |
| `hud-stdin-cache.json` | HUD 顯示快取，供介面層即時呈現任務概覽之用 |
| `agent-replay-d8b85d5d-7e2a-441d-9cb8-a491b39d1478.jsonl` | 代理事件回放日誌，逐行記錄代理動作以備溯查 |

## Subdirectories
| Directory | Purpose |
|-----------|---------|
| `sessions/` | 各工作階段之狀態快照，以階段識別碼為分野，各守其紀錄 |

## For AI Agents

### Working In This Directory
此目錄下諸檔，悉由 OMC 工具自動寫入，代理不得逕自手改。如需知悉任務現況，可讀 `mission-state.json`；如需查詢子代理，可覽 `subagent-tracking.json`；然修改之權，專屬於 OMC 工具，人與代理皆不應繞過工具直接覆寫。`.jsonl` 乃追加式日誌，不可截斷或刪行。`sessions/` 下之快照亦同，讀可，寫不可。違此者，恐致狀態錯亂，任務失序，編排崩壞。

<!-- MANUAL -->
