<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-05-09 | Updated: 2026-05-09 -->

# themes

## Purpose
此乃佈景主題之所。Composer 依 `installer-paths` 將 `type:wordpress-theme` 之套件置入此目錄；自製佈景主題亦於此開發維護。目錄以 `.gitkeep` 佔位，待主題安裝後方有實質內容。

## For AI Agents

### Working In This Directory
Composer 所管之佈景主題不可手動編輯，升級時將覆蓋之。自製主題應建立獨立子目錄，以主題 slug 命名，並視需要獨立納入版控或以 Composer path repository 管理。新增 Composer 主題：`composer require wpackagist-theme/{theme-slug}`。切換啟用主題於 WordPress 後台操作，或以 `wp theme activate {slug}` 指令執行。

### Common Patterns
- `composer require wpackagist-theme/{slug}` → 自動安裝至 `themes/{slug}/`
- 自製主題置於 `themes/{custom-theme-slug}/`，可獨立維護 git history
- 子主題同置此目錄，父主題須同時安裝

<!-- MANUAL -->
