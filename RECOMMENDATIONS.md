# Recommended Plugins and MCPs

## Plugins

### Auto-Update Setup

To update a plugin when a new version is available:

1. Run `/plugin` in Claude Code
2. Go to **Marketplaces** tab
3. Select "Update marketplace" (or enable "Enable auto-update")
4. Go to **Installed** tab
5. Select the plugin and choose "Update"
6. Restart Claude Code

---

### credo (Workflow Session Init)

> Opinionated workflow guides and best practices for Claude Code projects.
> Includes `/credo:session-init` for Main Agent orchestration setup.

**Repo:** https://github.com/Marcel-Bich/marcel-bich-claude-marketplace

**Install:**
```bash
claude plugin marketplace add Marcel-Bich/marcel-bich-claude-marketplace
claude plugin install credo@marcel-bich-claude-marketplace
```

**Key commands:**
- `/credo:session-init` - Initialize session with Main Agent workflow instructions
- `/credo:psalm` - Interactive guide to available topics and workflows

---

### dogma (Rules Enforcement)

> Intelligent sync of Claude instructions with enforcement hooks.
> Provides security hooks, linting, AI traces cleanup, and permissions system.

> **Note:** Enforcement hooks increase token consumption. Recommended for Claude Max 20x.

**Repo:** https://github.com/Marcel-Bich/marcel-bich-claude-marketplace

**Install:**
```bash
claude plugin marketplace add Marcel-Bich/marcel-bich-claude-marketplace
claude plugin install dogma@marcel-bich-claude-marketplace
```

**Key commands:**
- `/dogma:sync` - Sync Claude instructions from any source
- `/dogma:lint` - Project-agnostic linting on staged files
- `/dogma:permissions` - Configure Claude autonomy levels
- `/dogma:cleanup` - Find and fix AI-typical patterns

---

### hydra (Parallel Agents)

> Git Worktree management for parallel agent execution.
> Enables isolated working directories without Git conflicts.

**Repo:** https://github.com/Marcel-Bich/marcel-bich-claude-marketplace

**Install:**
```bash
claude plugin marketplace add Marcel-Bich/marcel-bich-claude-marketplace
claude plugin install hydra@marcel-bich-claude-marketplace
```

**Key commands:**
- `/hydra:create` - Create new worktree with its own branch
- `/hydra:parallel` - Start multiple agents in parallel across worktrees
- `/hydra:merge` - Merge worktree branch back
- `/hydra:help` - Show all commands

---

### Signal (Desktop Notifications)

> Desktop notifications showing what Claude Code is working on - even when terminal is not focused.
> Perfect for `--dangerously-skip-permissions` mode to monitor progress.

> **Features:**
> - Live status as desktop notification
> - Sound alerts on completion or when input needed
> - Optional: AI summaries via Haiku (costs API credits!)

> **Info:** Haiku summaries are disabled by default.

**Repo:** https://github.com/Marcel-Bich/marcel-bich-claude-marketplace

**Install:**
```bash
claude plugin marketplace add Marcel-Bich/marcel-bich-claude-marketplace
claude plugin install signal@marcel-bich-claude-marketplace
```

**Optional settings** in `~/.claude/settings.json`:
```json
{
  "env": {
    "CLAUDE_NOTIFY_HAIKU": "false",
    "CLAUDE_NOTIFY_SOUND_COMPLETE": "0.4",
    "CLAUDE_NOTIFY_SOUND_ATTENTION": "0.25"
  }
}
```

---

### Limit (Usage Statusline)

> Shows API usage in statusline.

**Repo:** https://github.com/Marcel-Bich/marcel-bich-claude-marketplace

**Install:**
```bash
claude plugin marketplace add Marcel-Bich/marcel-bich-claude-marketplace
claude plugin install limit@marcel-bich-claude-marketplace
```

---

### import (Documentation Import)

> Import external documentation locally with smart fallback chain.
> Bypasses AI-blocking sites using Context7 -> WebFetch -> Playwright.

**Repo:** https://github.com/Marcel-Bich/marcel-bich-claude-marketplace

**Install:**
```bash
claude plugin marketplace add Marcel-Bich/marcel-bich-claude-marketplace
claude plugin install import@marcel-bich-claude-marketplace
```

**Key commands:**
- `/import:url-or-path` - Import from URL or local path
- `/import:search` - Search within cached docs
- `/import:list` - List all cached documentation

---

### get-shit-done (GSD Installer)

> Installer for TACHES' Get-Shit-Done workflow system.
> Alternative to taches-cc-resources with project management focus.

**Repo:** https://github.com/Marcel-Bich/marcel-bich-claude-marketplace

**Install:**
```bash
claude plugin marketplace add Marcel-Bich/marcel-bich-claude-marketplace
claude plugin install get-shit-done@marcel-bich-claude-marketplace
```

**Setup:** Run `/gsd:setup` once, then restart Claude Code.

**Credits:** Original by [TACHES (glittercowboy)](https://github.com/glittercowboy/get-shit-done)

---

### Safety Net

> Blocks dangerous commands before execution - even in skip permission mode!
> Reduces risk when running automated tasks.

> **Warning:** Not a guarantee! AIs can sometimes find creative workarounds.
> Use at your own risk - but definitely better than running without it!

**Repo:** https://github.com/kenryu42/claude-code-safety-net

**Install:**
- Install as plugin from marketplace
- Restart Claude Code
- Test: prompt "execute: git checkout -- README.md" - should be blocked!

---

### taches-cc-resources (Meta-Engineering)

> Create incredibly good prompts that can be implemented nearly perfectly.
> Includes planning tools, skill creation, and more.

**Repo:** https://github.com/glittercowboy/taches-cc-resources

**Install:** Install as plugin from marketplace

**Key commands:**
- `/create-plan` - For new projects or plan creation
- `/run-plan` - Execute plans
- See github repo for "Recommended Workflow"

---

### Subagent Plugins (claude-plugins-official)

> These plugins provide the specialized agents that dogma references in its orchestration workflow.
> CLAUDE.subagents.md and dogma-orchestration mention agents like code-reviewer, code-architect,
> silent-failure-hunter - without these plugins installed, those agents will not be available.

**Repo:** https://github.com/anthropics/claude-plugins-official

#### feature-dev

> Code architecture and exploration agents.

**Agents:** code-architect, code-explorer, code-reviewer

**Install:**
```bash
claude plugin install feature-dev@claude-plugins-official
```

---

#### plugin-dev

> Plugin development agents.

**Agents:** agent-creator, plugin-validator, skill-reviewer

**Install:**
```bash
claude plugin install plugin-dev@claude-plugins-official
```

---

#### pr-review-toolkit

> Code review and analysis agents.

**Agents:** silent-failure-hunter, code-simplifier, comment-analyzer, code-reviewer, pr-test-analyzer, type-design-analyzer

**Install:**
```bash
claude plugin install pr-review-toolkit@claude-plugins-official
```

---

#### superpowers

> Advanced development skills and code review.

**Agents:** code-reviewer

**Install:**
```bash
claude plugin install superpowers@claude-plugins-official
```

---

## Linting & Formatting Tools

Language-specific tools for code quality. Install globally for personal use, locally for CI/CD.

### JavaScript/TypeScript

#### Prettier (Formatter)

> Opinionated code formatter. Enforces consistent style automatically.

**Docs:** https://prettier.io/

**Install (Global):**
```bash
npm install -g prettier
```

**Install (Local - recommended for projects):**
```bash
npm install -D prettier
```

**Usage:**
```bash
# Format file
prettier --write src/index.ts

# Check without modifying
prettier --check .
```

---

#### ESLint (Linter)

> Finds and fixes problems in JavaScript/TypeScript code.
> Catches bugs, enforces best practices, prevents common mistakes.

**Docs:** https://eslint.org/

**Install (Global):**
```bash
npm install -g eslint
```

**Install (Local - recommended for projects):**
```bash
npm install -D eslint
```

**Usage:**
```bash
# Lint files
eslint src/

# Auto-fix what's possible
eslint --fix src/
```

---

### Python

#### ruff (Linter + Formatter)

> Extremely fast Python linter and formatter written in Rust.
> Replaces flake8, isort, black, and many other tools.

**Docs:** https://docs.astral.sh/ruff/

**Install (Global - recommended):**
```bash
pip install ruff
# or
pipx install ruff
```

**Install (Local):**
```bash
pip install ruff
# Add to requirements-dev.txt or pyproject.toml
```

**Usage:**
```bash
# Lint
ruff check .

# Auto-fix
ruff check --fix .

# Format
ruff format .
```

---

### PHP

#### PHP-CS-Fixer (Formatter)

> Fixes PHP code style according to PSR standards.

**Docs:** https://cs.symfony.com/

**Install (Global):**
```bash
composer global require friendsofphp/php-cs-fixer
```

**Install (Local):**
```bash
composer require --dev friendsofphp/php-cs-fixer
```

**Usage:**
```bash
# Fix files
php-cs-fixer fix src/

# Dry run (show changes)
php-cs-fixer fix --dry-run --diff src/
```

---

#### PHPStan (Linter)

> Static analysis tool for PHP. Finds bugs without running code.

**Docs:** https://phpstan.org/

**Install (Global):**
```bash
composer global require phpstan/phpstan
```

**Install (Local - recommended):**
```bash
composer require --dev phpstan/phpstan
```

**Usage:**
```bash
# Analyze at level 5 (0-9, higher = stricter)
phpstan analyse src/ --level=5

# Use config file
phpstan analyse -c phpstan.neon
```

---

### Rust

#### rustfmt (Formatter)

> Official Rust formatter. Included with Rust toolchain.

**Docs:** https://rust-lang.github.io/rustfmt/

**Install:** Comes with `rustup`

**Usage:**
```bash
# Format project
cargo fmt

# Check without modifying
cargo fmt --check
```

---

#### Clippy (Linter)

> Official Rust linter. Catches common mistakes and suggests improvements.

**Docs:** https://doc.rust-lang.org/clippy/

**Install:** Comes with `rustup`, or:
```bash
rustup component add clippy
```

**Usage:**
```bash
# Run lints
cargo clippy

# Treat warnings as errors
cargo clippy -- -D warnings
```

---

### Go

#### gofmt (Formatter)

> Official Go formatter. Included with Go toolchain.

**Docs:** https://pkg.go.dev/cmd/gofmt

**Install:** Comes with Go

**Usage:**
```bash
# Format file (prints to stdout)
gofmt -w .

# Check without modifying
gofmt -l .
```

---

#### golangci-lint (Linter)

> Fast linters runner for Go. Aggregates many linters into one tool.

**Docs:** https://golangci-lint.run/

**Install (Global - recommended):**
```bash
# Linux/macOS
curl -sSfL https://raw.githubusercontent.com/golangci/golangci-lint/master/install.sh | sh -s -- -b $(go env GOPATH)/bin

# Or via go install
go install github.com/golangci/golangci-lint/cmd/golangci-lint@latest
```

**Usage:**
```bash
# Run lints
golangci-lint run

# With specific linters
golangci-lint run --enable=gofmt,govet,errcheck
```

---

## MCP Servers

### context7

> Enables searching current technical documentation on the web.
> Helps avoid outdated suggestions and hallucinations.

**Docs:** https://claudelog.com/claude-code-mcps/context7-mcp/

**Install (Linux/WSL):**
```bash
MCP_NAME="context7" MCP_CMD="npx" MCP_ARGS='["-y","@upstash/context7-mcp"]' node -e "const fs=require('fs'), path=require('path'); const p=path.join(process.env.HOME,'.claude.json'); let j={}; try{ j=JSON.parse(fs.readFileSync(p,'utf8')) }catch(e){ j={} } j.mcpServers = j.mcpServers || {}; j.mcpServers[process.env.MCP_NAME] = { command: process.env.MCP_CMD, args: JSON.parse(process.env.MCP_ARGS) }; fs.writeFileSync(p, JSON.stringify(j, null, 2));"
```

**Install (Windows PowerShell):**
```powershell
$env:MCP_NAME="context7"; $env:MCP_CMD="npx"; $env:MCP_ARGS='["-y","@upstash/context7-mcp"]'; node -e "const fs=require('fs'), path=require('path'); const p=path.join(process.env.USERPROFILE,'.claude.json'); let j={}; try{ j=JSON.parse(fs.readFileSync(p,'utf8')) }catch(e){ j={} } j.mcpServers = j.mcpServers || {}; j.mcpServers[process.env.MCP_NAME] = { command: process.env.MCP_CMD, args: JSON.parse(process.env.MCP_ARGS) }; fs.writeFileSync(p, JSON.stringify(j, null, 2));"
```

Restart Claude Code, then test:
```
Find out via mcp using current docs how XYZ is correctly implemented.
```

---

### Playwright

> Browser automation and testing via MCP.

**NPM:** https://www.npmjs.com/package/@playwright/mcp

**Install:** Follow package instructions, add to `~/.claude.json`

---

## Git Host Security Settings

> Built-in security features of git hosting platforms.
> Free for public repos, limited free features for private repos.
> Configure via web interface, not command line.

### GitHub (Public Repositories - All Free)

| Feature | Recommended | Description |
|---------|-------------|-------------|
| Private vulnerability reporting | Enabled | Community can privately report security issues |
| Dependency graph | Enabled | Shows all dependencies |
| Dependabot alerts | Enabled | Warns about vulnerabilities in dependencies |
| Dependabot security updates | Enabled | Auto-creates PRs for security fixes |
| Grouped security updates | Enabled | Groups security PRs together |
| CodeQL analysis | Enabled | Static code analysis for vulnerabilities |
| Copilot Autofix | On | AI suggestions for CodeQL fixes |
| Secret Protection | Enabled | Detects leaked secrets |
| Push protection | Enabled | Blocks commits containing secrets |

**NOT recommended:** Dependabot version updates (too spammy without user tests)

### GitHub (Private Repositories - Free Features Only)

| Feature | Recommended |
|---------|-------------|
| Dependency graph | Enabled |
| Dependabot alerts | Enabled |
| Dependabot security updates | Enabled |
| Grouped security updates | Enabled |

### GitLab

| Feature | Recommended | Description |
|---------|-------------|-------------|
| Dependency Scanning | Enabled | Scans dependencies for vulnerabilities |
| Secret Detection | Enabled | Detects leaked secrets in commits |
| SAST | Enabled | Static Application Security Testing |

### Bitbucket

| Feature | Recommended | Description |
|---------|-------------|-------------|
| Security Advisories | Enabled | Vulnerability alerts for dependencies |

### Setup URLs

| Host | Settings URL |
|------|--------------|
| GitHub | `https://github.com/{owner}/{repo}/settings/security_analysis` |
| GitLab | `https://gitlab.com/{owner}/{repo}/-/settings/security_and_compliance` |
| Bitbucket | `https://bitbucket.org/{owner}/{repo}/admin/security` |
