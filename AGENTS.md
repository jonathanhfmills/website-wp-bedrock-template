<!-- Generated: 2026-05-09 | Updated: 2026-05-09 -->

# website-wp-bedrock-template

## Purpose
此乃 WordPress Bedrock 之範本也。以 Composer 治依賴，以環境變數分設定，以 `web/` 為獨立網根，使新專案得循此式而立。凡欲創建 WordPress 新站者，複製此範本，依環境配置之，即可起工。

## Key Files
| File | Description |
|------|-------------|
| `composer.json` | 宣告依賴：`roots/bedrock` 與 `roots/wordpress`，並定插件、佈景主題之安裝路徑 |
| `wp-cli.yml` | 指定 WP-CLI 之網根與 WordPress 核心路徑 |
| `project.code-workspace` | VS Code 工作區設定 |

## Subdirectories
| Directory | Purpose |
|-----------|---------|
| `.devcontainer/` | 容器化開發環境之定義，供 VS Code Dev Containers 及 GitHub Codespaces 使用 |
| `.github/` | GitHub Actions 工作流程及倉庫設定 |
| `.omc/` | OMC 多代理協調器之狀態與計畫 |
| `.vscode/` | VS Code 編輯器設定 |
| `config/` | Bedrock 環境設定，分 `development`、`staging`、`production` 諸環境 |
| `web/` | 網站根目錄；含 `wp/`（WordPress 核心）、`app/`（插件、佈景主題）及 `wp-config.php` |

## For AI Agents

### Working In This Directory
此為範本倉庫，非正式站點。修改時須顧全範本之通用性，勿寫入特定站點之資料。環境敏感之設定（資料庫憑證、鹽值等）悉數置於 `.env`，此檔不入版本控制。WordPress 核心裝於 `web/wp/`，插件與佈景主題裝於 `web/app/` 之下，勿直接編輯 `web/wp/` 內之檔案。依賴之增刪一律透過 Composer，不可手動複製套件。

### Common Patterns
- 新增插件：`composer require wpackagist-plugin/{plugin-slug}`
- 新增佈景主題：`composer require wpackagist-theme/{theme-slug}`
- 升級 WordPress：更新 `composer.json` 中 `roots/wordpress` 之版本約束，執行 `composer update`
- WP-CLI 指令須在專案根目錄執行，`wp-cli.yml` 已自動指向正確路徑
- 環境設定存於 `config/environments/{environment}.php`，共用設定存於 `config/application.php`

## Dependencies

### External
| Package | Description |
|---------|-------------|
| `roots/bedrock` | Bedrock 框架本體，提供目錄結構、環境設定載入機制 |
| `roots/wordpress` | WordPress 核心，由 Composer 管理，安裝於 `web/wp/` |
| `composer/installers` | 使 Composer 能將插件與佈景主題裝至正確路徑 |
| `roots/wordpress-core-installer` | 使 WordPress 核心裝於指定之 `web/wp/` 目錄 |

## For AI Agents (Domain Language Maintenance)

### Domain Language Maintenance

AI agents working in this repo maintain living documentation inline as
decisions crystallise. Do not batch — capture as they happen.

**Challenge against the glossary.** When a term conflicts with an existing
definition in GLOSSARY.md, call it out immediately.

**Sharpen fuzzy language.** When vague or overloaded terms appear, propose
the canonical term from GLOSSARY.md.

**Cross-reference with code.** When behavior is stated, check whether the
code agrees. Surface contradictions immediately.

**Update docs inline.**
- Term resolved → add to GLOSSARY.md immediately.
  Format: alphabetical, one sentence per term, _Avoid_ line for aliases.
- Relationship or ambiguity resolved → update CONTEXT.md immediately.
  Format: Relationships (bold terms, cardinality), Example dialogue, Flagged ambiguities.
- Rejected framing or cross-cutting rule → add to LANGUAGE.md immediately.
  Format: Principles (imperatives), Rejected framings (why not + what instead).
- Domain experts only — never couple to implementation details.

**Create files lazily.** No CONTEXT.md → create when first relationship resolved.
No GLOSSARY.md → create when first term resolved. No LANGUAGE.md → create when
first rejected framing emerges. No docs/adr/ → create when first ADR needed.

**Migration.** If CONTEXT.md has a Language section, migrate all terms to
GLOSSARY.md at session start. Announce briefly, then proceed.

**Record ADRs for hard decisions.** ADRs are the immutable log that stops
decisions being re-litigated. Write immediately when a decision is: (1) hard
to reverse, (2) surprising without context, (3) result of a real trade-off.
Format: docs/adr/NNNN-slug.md — Status / Context / Decision / Considered
Options / Consequences. Never edit an existing ADR — write a new one that
supersedes it.

**Offer ROADMAP.md when milestones emerge.** When multi-month milestones or
outcomes not tracked in the issue tracker surface. Format: Vision / Phases
(Theme, Target month, milestones) / Current Focus.

<!-- MANUAL -->
