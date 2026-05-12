<!-- Generated: 2026-05-09 | Updated: 2026-05-09 -->

# Glossary

## Terms

| Term | Definition |
|------|-----------|
| **ABSPATH** | WordPress 核心之絕對路徑常數，定義為 `web/wp/`，由 `config/application.php` 末端設定。 |
| **Adminer** | 網頁介面之資料庫管理工具，以 Docker 容器運行，埠 8081 對外開放，僅供開發之用。 |
| **bedrock-autoloader** | Bedrock 提供之必載插件自動載入器，使安裝於 `mu-plugins/` 子目錄之插件亦能被 WordPress 自動載入。 |
| **Bedrock** | Roots 團隊所製之 WordPress 樣板框架，以 Composer 管理依賴，以環境變數分離設定，並將網根縮至 `web/` 目錄。 |
| **CONTENT_DIR** | WordPress 自訂內容目錄常數，值為 `/app`，用以指向 `web/app/` 而非預設之 `wp-content/`。 |
| **Config::apply()** | Bedrock `WPConfig` 類別之方法，將所有 `Config::define()` 所積累之常數一次寫入 WordPress 設定。 |
| **DATABASE_URL** | 以 DSN 字串形式提供資料庫連線資訊之環境變數，若設定則覆蓋個別 `DB_*` 變數。 |
| **DB_HOST** | 資料庫主機之環境變數，開發環境預設值為 `database`（Docker 服務名）。 |
| **devcontainer** | VS Code Dev Containers 規範所定義之容器化開發環境，以 `devcontainer.json` 為入口，統御 Docker Compose 諸服務。 |
| **Dotenv** | PHP 函式庫，讀取根目錄之 `.env`（及 `.env.local`）並將鍵值對載入為環境變數，供 `config/application.php` 取用。 |
| **env-setup.sh** | 初始化腳本之一，讀取環境變數範本，於容器建立時生成 `.env` 配置檔。 |
| **fastcgi_pass** | Nginx 設定指令，將 PHP 請求轉發至 PHP-FPM 之 TCP 套接字，此處指向 `wp:9000`。 |
| **GitHub Actions** | CI/CD 自動化平台，工作流程定義存於 `.github/workflows/`，掌部署與依賴更新二事。 |
| **GitHub Secrets** | GitHub 倉庫層級之加密密鑰儲存，工作流程以 `${{ secrets.NAME }}` 引用，憑證不落工作流程檔案。 |
| **grant-root.sql** | MariaDB 初始化 SQL 腳本，授予 root 帳號自任意主機連入之權，嚴限開發環境使用。 |
| **init.sh** | `.devcontainer/scripts/` 之主入口腳本，由 `postCreateCommand` 調用，依序執行所有初始化子腳本。 |
| **installer-paths** | `composer.json` 中 `extra` 區塊之設定，指定各類型套件（插件、佈景主題、必載插件）之安裝目標目錄。 |
| **MariaDB** | 關聯式資料庫管理系統，版本 10.11.13，以 Docker 容器運行，埠 3307 對外開放，資料以具名卷 `db` 持久化。 |
| **mkcert** | 本地可信 SSL 憑證生成工具，由 `init.sh` 調用，生成之憑證存於 `nginx/ssl/`，供本地 HTTPS 開發之用。 |
| **mu-plugins** | Must-Use Plugins 之縮寫，即必載插件；置於此目錄之插件 WordPress 啟動時自動載入，無從後台停用。 |
| **Nginx** | 反向代理伺服器，版本 1.29.2，以 Docker 容器運行，負責 TLS 終結、HTTP 重定向及 PHP 請求轉發。 |
| **OMC** | oh-my-claudecode 之縮寫，多代理編排層；其狀態存於 `.omc/`，不可手動修改。 |
| **PHP-FPM** | PHP FastCGI Process Manager，以 `php:8.2-fpm` 映像運行，執行 WordPress 應用程式邏輯，監聽埠 9000。 |
| **postCreateCommand** | `devcontainer.json` 之鉤子，容器建立後執行一次，此處調用 `scripts/init.sh` 完成環境初始化。 |
| **roots/bedrock** | Composer 套件，版本 1.28.4，提供 Bedrock 框架之目錄結構與設定載入機制。 |
| **roots/wordpress** | Composer 套件，版本約束 `^6.9`，WordPress 核心由此管理，安裝於 `web/wp/`。 |
| **roots/wordpress-core-installer** | Composer 插件，使 WordPress 核心安裝至 `composer.json` `extra.wordpress-install-dir` 所指定之路徑。 |
| **WP_CONTENT_DIR** | WordPress 常數，指向 `web/app/`，覆蓋預設之 `wp-content/` 路徑。 |
| **WP_ENV** | 環境識別常數，值為 `production`、`staging`、`development` 之一，決定載入哪個環境覆寫設定檔。 |
| **WP_HOME** | WordPress 站點首頁 URL 常數，為必填環境變數，由 `.env` 注入。 |
| **WP_SITEURL** | WordPress 核心安裝 URL 常數，為必填環境變數，由 `.env` 注入，通常為 `WP_HOME/wp`。 |
| **wp-cli.yml** | WP-CLI 設定檔，指定網根與 WordPress 核心路徑，使 WP-CLI 指令可於專案根目錄正確執行。 |
| **wp-config.php** | WordPress 必需之設定入口檔；於 Bedrock 架構中僅作轉接之用，載入 `vendor/autoload.php` 與 `config/application.php`。 |
| **WPConfig** | Bedrock 之設定管理類別（`Roots\WPConfig\Config`），以 `define()` 積累常數，以 `apply()` 統一寫入。 |

<!-- MANUAL -->
