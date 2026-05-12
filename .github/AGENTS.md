<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-05-09 | Updated: 2026-05-09 -->

# .github

## Purpose
此目錄乃持續整合與持續部署之樞紐也。以 GitHub Actions 為引擎，掌自動化測試、依賴更新、遠端佈署諸事。凡推送代碼或開立拉取請求，流程自動觸發，無需人手干預。

## Key Files
| File | Description |
|------|-------------|
| `config.yml` | GitHub Apps 之設定，管倉庫層級之應用程式整合 |
| `dependabot.yml` | 自動依賴更新之設定；Dependabot 定期掃描，若有新版則開立拉取請求 |

## Subdirectories
| Directory | Purpose |
|-----------|---------|
| `workflows/` | GitHub Actions 工作流程定義；含 `deploy.yml`（佈署流水線）與 `wp-deps.yml`（WordPress 依賴更新流水線） |

## For AI Agents

### Working In This Directory
修改工作流程時，須驗證 YAML 語法之正確性，縮排一字之差即令流程失效。密鑰與憑證悉數存於 GitHub Secrets，不可硬寫於工作流程檔案之內。`deploy.yml` 涉及遠端伺服器操作，改動前須細審觸發條件與環境保護規則，以防誤佈署至生產環境。`dependabot.yml` 之更新頻率與目標目錄，應與專案實際依賴管理方式相符。

### Common Patterns
- 新增工作流程：於 `workflows/` 下建立 `.yml` 檔，以 `on:` 定義觸發條件
- 傳遞密鑰至步驟：用 `${{ secrets.SECRET_NAME }}` 語法引用，不可直接寫值
- 依賴 Composer 之步驟：先快取 `~/.composer/cache` 以加速執行
- 佈署工作流程通常依賴分支名稱（如 `main` 觸發生產佈署）或手動觸發（`workflow_dispatch`）

<!-- MANUAL -->
