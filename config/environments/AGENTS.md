<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-05-09 | Updated: 2026-05-09 -->

# environments

## Purpose
此目錄專司各環境之差異覆寫設定。凡與 `application.php` 相異者，方才於此著筆；共用之邏輯，概不重書。開發境以除錯為要，預備境模擬正式以驗部署，生產境之設定則由伺服器環境變數注入，不落文件。

## Key Files
| File | Description |
|------|-------------|
| `development.php` | 本地開發環境之覆寫設定；開啟除錯模式、指定本地資料庫，寬容以待開發便利 |
| `staging.php` | 預備環境之覆寫設定；模擬正式部署條件，供上線前驗收之用 |

## For AI Agents

### Working In This Directory
此目錄之設定，僅書寫與 `application.php` 相異之部分，不可複述共用邏輯。`development.php` 可開除錯、放寬快取，然此類設定絕不可流入 `staging.php` 或主設定。敏感憑證不論在何環境，皆不得硬寫於此，必須透過 `.env` 以環境變數注入。生產環境無對應之檔，乃屬刻意之設計，不可於此新建 `production.php`；生產設定之職，在於伺服器與 `.env`，非此目錄所轄。新增環境時，於此建立對應之 `.php`，並確認 `application.php` 能正確載入之。

<!-- MANUAL -->
