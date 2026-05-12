<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-05-09 | Updated: 2026-05-09 -->

# nginx

## Purpose
此目錄藏 Nginx 反向代理容器之設定。`default.conf` 定義伺服器區塊，將 PHP 請求轉發至 PHP-FPM，並處理 HTTP 至 HTTPS 之重定向。`ssl/` 子目錄為本機 TLS 憑證之存放處，憑證由 mkcert 生成，供本地 HTTPS 開發之用。

## Key Files
| File | Description |
|------|-------------|
| `default.conf` | Nginx 伺服器區塊設定，含反向代理規則、PHP-FPM 上游指向及 SSL 憑證路徑 |

## Subdirectories
| Directory | Purpose |
|-----------|---------|
| `ssl/` | 存放本機 TLS 憑證與私鑰，由 mkcert 生成；目錄現為空，憑證須於容器初始化後手動或由腳本置入 |

## For AI Agents

### Working In This Directory
`default.conf` 掛入容器之 `/etc/nginx/conf.d/`，修改後須重啟 Nginx 容器方生效。PHP 請求藉 `fastcgi_pass` 指向 `wp` 服務之 9000 埠，服務名稱須與 `docker-compose.yml` 所定義之服務名一致。SSL 憑證路徑於 `default.conf` 中硬編碼，憑證檔名須與設定相符；若更改憑證檔名，須同步修改 `default.conf`。`ssl/` 目錄現為空佔位，憑證由 `scripts/init.sh` 中之 mkcert 命令生成並置入，勿將真實憑證提交至版本控制。

<!-- MANUAL -->
