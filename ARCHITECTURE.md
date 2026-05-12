<!-- Generated: 2026-05-09 | Updated: 2026-05-09 -->

# Architecture

## Overview

此乃 WordPress Bedrock 範本之結構圖，客觀錄其組件、關係、資料流向與技術選擇，供後人取法。

## Layer Diagram

```
┌─────────────────────────────────────────────────────┐
│                   外部請求 (HTTP/HTTPS)               │
└──────────────────────────┬──────────────────────────┘
                           ▼
┌─────────────────────────────────────────────────────┐
│         Nginx (nginx:1.29.2)  反向代理層              │
│  • HTTP→HTTPS 重定向                                  │
│  • mkcert 本地 SSL 憑證 (ssl/)                        │
│  • fastcgi_pass → wp:9000                            │
└──────────────────────────┬──────────────────────────┘
                           ▼
┌─────────────────────────────────────────────────────┐
│         PHP-FPM 應用層 (php:8.2-fpm)                  │
│                                                     │
│  web/index.php                                      │
│    └─ define WP_USE_THEMES → web/wp/wp-blog-header  │
│                                                     │
│  web/wp-config.php                                  │
│    ├─ vendor/autoload.php       (Composer 自動載入)  │
│    ├─ config/application.php    (主設定)              │
│    └─ web/wp/wp-settings.php    (WordPress 核心啟動) │
│                                                     │
│  config/application.php                             │
│    ├─ Dotenv: 載入 .env / .env.local                │
│    ├─ 定義常數: WP_ENV, WP_HOME, WP_SITEURL          │
│    ├─ 定義常數: CONTENT_DIR=/app                     │
│    ├─ 定義常數: WP_CONTENT_DIR=web/app/              │
│    ├─ 資料庫: DB_NAME/USER/PASSWORD/HOST             │
│    ├─ 認證鹽值: 八組 KEY/SALT                        │
│    ├─ 載入 config/environments/{WP_ENV}.php          │
│    └─ Config::apply()                               │
│                                                     │
│  config/environments/                               │
│    ├─ development.php  (除錯開啟、本地覆寫)           │
│    └─ staging.php      (模擬生產、驗收用)             │
│    [production: 無對應檔，由環境變數全權掌管]          │
└──────────────────────────┬──────────────────────────┘
                           ▼
┌─────────────────────────────────────────────────────┐
│                WordPress 核心層                       │
│  web/wp/           ← Composer 安裝 roots/wordpress  │
│  web/app/          ← wp-content 等價目錄             │
│    ├─ mu-plugins/  ← 必載插件 (bedrock-autoloader)   │
│    ├─ plugins/     ← 標準插件 (Composer/手動)        │
│    ├─ themes/      ← 佈景主題                        │
│    └─ uploads/     ← 使用者媒體 (不入版控)           │
└──────────────────────────┬──────────────────────────┘
                           ▼
┌─────────────────────────────────────────────────────┐
│              MariaDB 10.11.13 資料庫層               │
│  • 埠 3307:3306 (對外)                               │
│  • db volume 持久化                                  │
│  • grant-root.sql: 僅開發用之寬泛授權                 │
│  • mysql/default.conf: 字元集、連線、緩衝覆寫         │
└─────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────┐
│              Adminer (adminer:latest)                │
│  • 埠 8081 → 資料庫管理介面                           │
│  • depends_on: database                              │
└─────────────────────────────────────────────────────┘
```

## Dependency Management

```
composer.json
  └─ roots/bedrock  1.28.4
       ├─ composer/installers       → 決定安裝路徑
       └─ roots/wordpress-core-installer → 核心裝於 web/wp/
  └─ roots/wordpress ^6.9          → 安裝於 web/wp/
  └─ installer-paths:
       web/app/mu-plugins/{$name}/  ← type:wordpress-muplugin
       web/app/plugins/{$name}/     ← type:wordpress-plugin
       web/app/themes/{$name}/      ← type:wordpress-theme
```

## CI/CD Pipeline

```
GitHub Push / workflow_dispatch
  └─ .github/workflows/
       ├─ deploy.yml     → SSH/rsync → 遠端伺服器
       └─ wp-deps.yml    → Composer install / 插件更新
  └─ dependabot.yml      → 自動依賴更新拉取請求
```

## devcontainer Initialization Flow

```
VS Code / Codespaces
  └─ devcontainer.json
       ├─ dockerComposeFile: docker-compose.yml
       ├─ service: wordpress (wp)
       ├─ workspaceFolder: /var/www/html
       ├─ mounts:
       │    .claude      → /root/.claude
       │    .claude.json → /root/.claude.json
       │    ~/.ssh       → /var/www/html/.ssh
       └─ postCreateCommand:
            └─ scripts/init.sh
                 ├─ env-setup.sh       → 生成 .env
                 ├─ git-credentials.sh → Git 憑證助手
                 └─ git-workflow-setup.sh → Git 鉤子與別名
```

## Key Boundary Decisions

| 決策 | 說明 |
|------|------|
| `web/wp/` 為 Composer 自動生成域 | 不可手動編輯，升級時覆蓋 |
| `web/app/` 代替 `wp-content/` | 隔離核心與內容，降低升級衝突 |
| `config/` 與 `web/` 分離 | 設定不暴露於網根，增強安全性 |
| 無 `production.php` | 生產設定全由環境變數注入，強制不落文件 |
| `.env` 不入版控 | 憑證與鹽值以環境變數隔離，範本用 `.env.example` 替代 |
| `mu-plugins/bedrock-autoloader.php` | 支援子目錄式必載插件，彌補 WordPress 原生限制 |
| Nginx 終結 SSL | PHP-FPM 不直接對外，由 Nginx 代理並處理 TLS |

<!-- MANUAL -->
