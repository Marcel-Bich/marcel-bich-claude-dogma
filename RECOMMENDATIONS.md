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
