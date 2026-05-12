<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-05-09 | Updated: 2026-05-09 -->

# .devcontainer

## Purpose
此目錄乃開發容器之樞紐，以 Docker Compose 統御諸服務，為 WordPress Bedrock 開發環境提供完整基礎。其中 PHP-FPM 執行應用程式邏輯，Nginx 充反向代理並終結 SSL，MariaDB 掌管資料庫，Adminer 供資料庫管理之用。VS Code 透過 `devcontainer.json` 接入此環境，令開發者得以在容器內一體作業。

## Key Files
| File | Description |
|------|-------------|
| `Dockerfile` | 以 `php:8.2-fpm` 為基礎，安裝 PHP 擴充、Composer、WP-CLI、GitHub CLI 及 mkcert，構建 WordPress 開發映像 |
| `devcontainer.json` | 定義 VS Code 開發容器體驗：指定服務、工作目錄、掛載點、擴充功能及容器啟動後命令 |
| `docker-compose.yml` | 編排四服務：`wp`（PHP-FPM）、`nginx`（反向代理）、`database`（MariaDB）、`adminer_csm`（資料庫管理介面） |

## Subdirectories
| Directory | Purpose |
|-----------|---------|
| `mysql/` | 存放 MariaDB 設定檔及初始化 SQL，包含授予 root 遠端存取之腳本 |
| `nginx/` | 存放 Nginx 虛擬主機設定及本機 SSL 憑證，負責 HTTP 至 HTTPS 重定向與反向代理 |
| `php/` | 存放 PHP 執行期設定（`php.ini`）及 PHP-FPM 進程池設定（`www.conf`） |
| `scripts/` | 存放容器初始化腳本，由 `postCreateCommand` 於容器建立後執行 |

## For AI Agents

### Working In This Directory
修改此目錄時，須知四服務相互依存：`nginx` 依賴 `wp`，`wp` 與 `adminer_csm` 均依賴 `database`。凡更動 `Dockerfile`，必重新構建映像，不可僅重啟容器。`devcontainer.json` 所定義之掛載點將宿主機之 `.claude`、`.claude.json` 及 `.ssh` 掛入容器，修改掛載設定時須確認宿主路徑存在。`postCreateCommand` 執行 `scripts/init.sh`，若新增初始化邏輯，應於此腳本內擴充，勿直接修改 `devcontainer.json` 之命令字串。埠號映射：HTTP 80、HTTPS 443 綁定本機迴環，MariaDB 對外開放 3307，Adminer 開放 8081。

### Common Patterns
- 新增 PHP 擴充：於 `Dockerfile` 中增加 `docker-php-ext-install` 指令，並於 `php/php.ini` 補充對應設定。
- 調整 Nginx 虛擬主機：修改 `nginx/default.conf`，SSL 憑證置於 `nginx/ssl/`，由 mkcert 生成。
- 資料庫初始化邏輯：增添 SQL 檔於 `mysql/`，Docker Compose 依字母順序執行 `docker-entrypoint-initdb.d/` 內之腳本。
- 新增 VS Code 擴充功能：於 `devcontainer.json` 之 `customizations.vscode.extensions` 陣列中追加擴充識別碼。
- 環境變數：資料庫憑證定義於 `docker-compose.yml` 之 `environment` 區塊，開發環境預設使用 `root`/`root`，正式環境務必替換。

## Dependencies

### External
- `php:8.2-fpm` — 官方 PHP Docker 映像，為 WordPress 執行基礎
- `nginx:1.29.2` — 官方 Nginx 映像，充反向代理
- `mariadb:10.11.13` — MariaDB 資料庫映像
- `adminer:latest` — 網頁資料庫管理工具
- `composer:2` — 依賴管理器，於 `Dockerfile` 多階段構建中複製可執行檔
- `ghcr.io/devcontainers/features/node:1` — VS Code devcontainer 功能，安裝 Node.js
- `ghcr.io/anthropics/devcontainer-features/claude-code:1.0` — VS Code devcontainer 功能，安裝 Claude Code CLI
- `mkcert` — 本機 SSL 憑證生成工具，由 `filippo.io` 提供
- `wp-cli` — WordPress 命令列管理工具
- `gh` — GitHub CLI，用於容器內 Git 操作

<!-- MANUAL -->
