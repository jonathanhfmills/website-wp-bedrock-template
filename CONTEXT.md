<!-- Generated: 2026-05-09 | Updated: 2026-05-09 -->

# Context

## Relationships

| 關係 | 說明 |
|------|------|
| **Nginx** → **PHP-FPM** (1:1) | Nginx 以 `fastcgi_pass wp:9000` 將所有 PHP 請求轉發至 `wp` 服務，二者同屬 Docker 網路，服務名須一致 |
| **PHP-FPM** → **MariaDB** (n:1) | `wp` 服務以 `DB_HOST=database` 連接資料庫，憑證由 `docker-compose.yml` 環境區塊或 `.env` 注入 |
| **Adminer** → **MariaDB** (n:1) | `adminer_csm` 以 `ADMINER_DEFAULT_SERVER=database` 指向同一資料庫服務 |
| **`web/index.php`** → **`web/wp/`** (1:1) | `index.php` 僅含兩行：定義主題旗標，載入 `wp-blog-header.php` 啟動 WordPress |
| **`web/wp-config.php`** → **`config/application.php`** (1:1) | `wp-config.php` 為純轉接橋樑，不含任何實質設定，全委 `application.php` |
| **`config/application.php`** → **`.env`** (1:1) | Dotenv 載入環境變數，`.env.local` 可覆蓋 `.env`；`WP_HOME`、`WP_SITEURL` 為必填 |
| **`config/application.php`** → **`config/environments/{WP_ENV}.php`** (1:0..1) | 依 `WP_ENV` 常數動態載入環境覆寫；生產環境無對應檔，此為刻意設計 |
| **`composer.json`** → **`web/wp/`** (1:1) | `roots/wordpress-core-installer` 將 WordPress 核心置於 `web/wp/`，Composer 全權管理 |
| **`composer.json`** → **`web/app/`** (1:n) | `composer/installers` 依 `installer-paths` 將插件、佈景主題、必載插件分置子目錄 |
| **`bedrock-autoloader.php`** → **`web/app/mu-plugins/`** (1:n) | 掃描必載插件子目錄，補 WordPress 僅能自動載入頂層檔案之限制 |
| **`scripts/init.sh`** → 諸初始化腳本 (1:n) | 為 `env-setup.sh`、`git-credentials.sh`、`git-workflow-setup.sh` 之統一入口，由 `postCreateCommand` 調用 |
| **devcontainer.json** → **docker-compose.yml** (1:1) | 宣告 `dockerComposeFile` 指向同目錄之 `docker-compose.yml`，VS Code 據此啟動容器群 |
| **GitHub Actions** → **遠端伺服器** (1:n) | `deploy.yml` 以 SSH/rsync 部署，憑證存於 GitHub Secrets，不落工作流程檔案 |

## Example: Request Flow

```
瀏覽器 HTTPS 請求
  → Nginx (127.0.0.1:443) 終結 TLS
  → fastcgi_pass wp:9000
  → PHP-FPM 執行 web/index.php
  → 載入 wp-blog-header.php (WordPress 核心)
  → WordPress 查詢 MariaDB (host: database, port: 3306)
  → 渲染輸出 → Nginx → 瀏覽器
```

## Example: Composer Plugin Install

```
composer require wpackagist-plugin/akismet
  → composer/installers 讀取 installer-paths
  → 插件安裝至 web/app/plugins/akismet/
  → WordPress 後台可見並啟用
```

## Flagged Ambiguities

| 項目 | 模糊之處 | 現狀 |
|------|---------|------|
| `devcontainer.json` 中 `service: wordpress` | `docker-compose.yml` 服務名為 `wp`，非 `wordpress`，二者不符 | 潛在錯誤，VS Code 啟動容器時恐無法定位服務 |
| `devcontainer.json` 中 `forwardPorts: [80, 8080]` | `docker-compose.yml` 未定義 8080 埠；Adminer 開放 8081，Nginx 開放 80/443 | 8080 轉發無對應服務，恐為過時殘留 |
| 生產環境鹽值來源 | `config/application.php` 以 `env()` 讀取八組鹽值，若 `.env` 未填則值為 `null` | 新站未設鹽值時安全性存疑，範本應有更明確之警示或預設生成機制 |
| `uploads/` 部署策略 | 明文不入版控，然部署流程 (`deploy.yml`) 如何同步媒體檔案未有定義 | CI/CD 範本中此部分屬未決事項 |
| `DATABASE_URL` 與個別 `DB_*` 變數並存 | `application.php` 支援兩種資料庫設定格式，`DATABASE_URL` 優先覆蓋個別變數 | 若二者同時存在，行為雖已定義，然易令新開發者困惑 |

<!-- MANUAL -->
