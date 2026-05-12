<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-05-09 | Updated: 2026-05-09 -->

# php

## Purpose
此目錄藏 PHP-FPM 容器之設定。`php.ini` 掌管 PHP 執行期參數，如記憶體上限、上傳大小及錯誤回報等級。`www.conf` 定義 FPM 進程池，規定工作程序數量、監聽套接字及請求佇列，決定應用程式之並發處理能力。

## Key Files
| File | Description |
|------|-------------|
| `php.ini` | PHP 執行期設定，覆蓋預設值，含記憶體限制、檔案上傳大小、執行逾時及錯誤顯示等參數 |
| `www.conf` | PHP-FPM 進程池設定，定義 `www` 池之監聽位址、工作程序管理模式（`dynamic`/`static`）及子程序數量上下限 |

## For AI Agents

### Working In This Directory
`php.ini` 掛入容器之 `/usr/local/etc/php/conf.d/`，`www.conf` 掛入 `/usr/local/etc/php-fpm.d/`，覆蓋映像內之預設值。修改任一檔案後，須重啟 `wp` 服務方生效；更動 `Dockerfile` 則須重新構建映像。調整 `www.conf` 之工作程序數時，須衡量宿主機可用記憶體，開發環境無需設定過高。`php.ini` 中 `upload_max_filesize` 與 `post_max_size` 須同步調整，且 Nginx 之 `client_max_body_size` 亦須配合修改，三者須保持一致。

<!-- MANUAL -->
