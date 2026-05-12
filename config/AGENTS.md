<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-05-09 | Updated: 2026-05-09 -->

# config

## Purpose
此目錄統攝 WordPress Bedrock 之應用程式設定。共用之基礎設定居於 `application.php`，各環境之差異覆寫則分置 `environments/` 子目錄之下。依此分層之法，生產、預備、開發三境各得其宜，而共用邏輯不必重複。

## Key Files
| File | Description |
|------|-------------|
| `application.php` | 主設定檔；定義路徑常數、載入 `.env` 環境變數、配置資料庫連線及 WordPress 核心選項，為一切環境之共同基礎 |

## Subdirectories
| Directory | Purpose |
|-----------|---------|
| `environments/` | 各環境之覆寫設定；內含 `development.php`、`staging.php` 等，僅載入與 `application.php` 相異之選項 |

## For AI Agents

### Working In This Directory
`application.php` 為生產設定之基準，修改時須假設此檔運行於正式環境，不可引入僅宜開發之設定。環境專屬之調整（如開啟除錯模式、放寬快取策略）一律寫入 `environments/` 下對應之檔，不可混入主設定。敏感憑證（資料庫密碼、鹽值）不得硬寫於此目錄任何檔案之中，必須透過 `.env` 以環境變數注入。新增環境時，於 `environments/` 下建立對應之 `.php` 檔，並於 `application.php` 確認其能被正確載入。

<!-- MANUAL -->
