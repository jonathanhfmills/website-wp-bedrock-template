<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-05-09 | Updated: 2026-05-09 -->

# app

## Purpose
此乃 Bedrock 所設之 `wp-content` 等價目錄也。凡插件、佈景主題、必載插件及上傳媒體，悉聚於此。Composer 統轄其依賴，版本皆錄於根目錄之 `composer.json`，不可於此目錄散置未受管之套件。

## Subdirectories
| Directory | Purpose |
|-----------|---------|
| `mu-plugins/` | 必載插件之所；WordPress 自動載入，無需後台啟用；含 `bedrock-autoloader.php` 以支援子目錄式必載插件 |
| `plugins/` | 標準插件之所；可由 Composer 管理，亦可手動置入 |
| `themes/` | 佈景主題之所；專案主題於此開發維護 |
| `uploads/` | 使用者上傳媒體之所；不入版本控制 |

## For AI Agents

### Working In This Directory
此目錄之下，切勿直接置入任何檔案，所有內容皆應歸於對應之子目錄。`uploads/` 已列於 `.gitignore`，不可強行納入版本控制。Composer 所管之插件與佈景主題，其程式碼由套件管理器生成，不可手動編輯，蓋更新時將覆蓋之。若需修改 Composer 管理之套件，應以 fork 或 patch 之法處置，勿直接改動 `plugins/` 或 `themes/` 內之供應商代碼。

### Common Patterns
- 新增插件，於根目錄之 `composer.json` 定義依賴，執行 `composer require` 以安裝，Composer 將自動置入 `plugins/{plugin-slug}/`
- 新增佈景主題，同以 Composer 管理，或於 `themes/` 下手動建立自製佈景主題目錄
- 必載插件置於 `mu-plugins/`，由 `bedrock-autoloader.php` 支援子目錄結構，無需逐一列於後台
- `uploads/` 之內容由 WordPress 運行時生成，本地開發環境可自行填充，部署時不隨版本庫傳遞

<!-- MANUAL -->
