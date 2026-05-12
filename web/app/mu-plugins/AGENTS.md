<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-05-09 | Updated: 2026-05-09 -->

# mu-plugins

## Purpose
此乃 WordPress 必載插件之所。凡置於此目錄之插件，WordPress 啟動時自動載入，先於一般插件，且無從後台停用。`bedrock-autoloader.php` 為 Bedrock 所設之自動載入器，使以 Composer 安裝於子目錄中之必載插件，亦能如標準必載插件般正常載入。

## Key Files
| File | Description |
|------|-------------|
| `bedrock-autoloader.php` | Bedrock 必載插件自動載入器；掃描子目錄中之插件，使其得以被 WordPress 自動載入，無需逐一置於頂層目錄 |

## For AI Agents

### Working In This Directory
`bedrock-autoloader.php` 乃 Bedrock 核心功能之一，不可修改、刪除或替換，蓋其破壞將致子目錄式必載插件悉數失效。如需新增必載插件，可直接置頂層 `.php` 檔，或建子目錄並放入插件主檔，`bedrock-autoloader.php` 將自動發現之。必載插件無停用機制，置入即生效，代理於此操作時須格外審慎，確認插件邏輯正確方可提交。Composer 所管之必載插件不可在此目錄手動編輯，當依套件管理器之法處置。

<!-- MANUAL -->
