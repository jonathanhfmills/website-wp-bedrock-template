<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-05-09 | Updated: 2026-05-09 -->

# workflows

## Purpose
此目錄存 GitHub Actions 工作流程定義。凡代碼推送或手動觸發，流程自動運行，掌佈署與 WordPress 依賴管理二事，使持續整合與持續交付得以無人值守。

## Key Files
| File | Description |
|------|-------------|
| `deploy.yml` | 佈署流水線；通常以 SSH 或 rsync 將構建產物推送至遠端伺服器，生產環境觸發條件須審慎設定 |
| `wp-deps.yml` | WordPress 依賴管理流水線；執行 Composer 安裝，並視需要更新插件及相關套件 |

## For AI Agents

### Working In This Directory
修改工作流程前，須細審觸發條件，尤其 `deploy.yml` 涉及生產伺服器，誤觸則害及線上環境。所有密鑰、憑證、伺服器地址悉數引用 `${{ secrets.SECRET_NAME }}`，不得硬寫於檔案之內。YAML 縮排須嚴格一致，差一格則流程失效。Composer 相關步驟應快取 `~/.composer/cache` 以縮短執行時間。新增步驟時，確認所需 Secrets 已於倉庫設定中預先配置。

<!-- MANUAL -->
