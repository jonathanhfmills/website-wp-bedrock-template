<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-05-09 | Updated: 2026-05-09 -->

# .omc

## Purpose
此目錄乃 OMC（oh-my-claudecode）編排層之狀態倉庫。凡持久化之專案脈絡、工作階段紀錄、任務狀態，皆藏於此。非人工撰寫之所，乃工具自理之域。

## Key Files
| File | Description |
|------|-------------|
| `project-memory.json` | 儲存專案持久脈絡，供諸智能代理取用，以明專案之歷史與要務。 |

## Subdirectories
| Directory | Purpose |
|-----------|---------|
| `sessions/` | 存工作階段 JSON 狀態檔，以 UUID 命名，由 OMC 工具自動寫入 |
| `state/` | 存工作階段追蹤、HUD 快取、任務狀態諸般紀錄，由 OMC 工具自行維護 |

## For AI Agents

### Working In This Directory
此目錄內諸檔，皆由 OMC 工具自動生成與更新，代理不得手動修改 `state/` 下任何檔案，亦不得擅改 `project-memory.json` 之結構。如需讀取專案脈絡，可取用 `project-memory.json`；如需更新，須假 OMC 工具之手，不可直書覆寫。凡違此例者，恐致狀態錯亂，編排失序。

<!-- MANUAL -->
