<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-05-09 | Updated: 2026-05-09 -->

# web

## Purpose
此乃網站之根目錄也。Bedrock 之設計，將 WordPress 核心移出網根之外，以固安防。外部請求由此入，經 `index.php` 引導，入於 WordPress 之流程。設定之載入、環境之切換，皆藉 `wp-config.php` 轉接 Bedrock 之機制而行。插件、佈景主題、必載插件及上傳檔案，悉數置於 `app/` 之下，此即 `wp-content` 之等價目錄也。

## Key Files
| File | Description |
|------|-------------|
| `index.php` | WordPress 啟動引導之入口，載入核心，開始請求之處理 |
| `wp-config.php` | 轉接設定之橋樑，載入 Bedrock 之 `config/application.php`，定義常數以指向正確路徑 |

## Subdirectories
| Directory | Purpose |
|-----------|---------|
| `app/` | `wp-content` 之等價目錄；含佈景主題、插件、必載插件及上傳檔案 |

## For AI Agents

### Working In This Directory
此目錄乃伺服器所指之網根，非 WordPress 核心所在。`web/wp/` 由 Composer 自動生成，切勿手動編輯其內之任何檔案，蓋升級時將悉數覆蓋也。`wp-config.php` 僅作路徑轉接之用，實質設定皆在 `config/` 之下，勿於此處直寫資料庫憑證或鹽值。新增或修改功能，應入 `app/` 之目錄，不可於此根目錄散置檔案。

### Common Patterns
- 佈景主題置於 `app/themes/{theme-slug}/`，插件置於 `app/plugins/{plugin-slug}/`
- 必載插件置於 `app/mu-plugins/`，隨 WordPress 自動載入，無需於後台啟用
- 上傳檔案存於 `app/uploads/`，此目錄不入版本控制
- 修改 `wp-config.php` 之需求極稀，若需新增常數，應於 `config/application.php` 或對應環境檔中定義之

<!-- MANUAL -->
