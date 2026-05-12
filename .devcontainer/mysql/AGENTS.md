<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-05-09 | Updated: 2026-05-09 -->

# mysql

## Purpose
此目錄藏 MariaDB 容器之設定。`default.conf` 規定資料庫伺服器啟動之參數，`grant-root.sql` 則於初始化時授予 root 帳號自任意主機連入之權，僅供開發之用，切勿移植正式環境。

## Key Files
| File | Description |
|------|-------------|
| `default.conf` | MySQL 伺服器設定檔，覆蓋預設參數，如字元集、連線逾時及緩衝區大小 |
| `grant-root.sql` | 初始化 SQL 腳本，授予 root 帳號自任意主機（`%`）連入之權，僅限開發環境 |

## For AI Agents

### Working In This Directory
此目錄之檔案由 Docker Compose 掛入 MariaDB 容器。`default.conf` 掛於 `/etc/mysql/conf.d/`，容器啟動時自動載入。`grant-root.sql` 置於 `docker-entrypoint-initdb.d/`，僅於資料庫**首次初始化**時執行，若資料卷已存，修改此檔不生效，須銷毀資料卷重建方可。多個 SQL 初始化檔依字母順序執行，命名時須留意順序。`grant-root.sql` 授予之權限寬泛，嚴禁搬入正式環境。

<!-- MANUAL -->
