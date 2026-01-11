# marcel-bich-claude-dogma

Public source of truth for Claude Code guidelines and configurations.

## Purpose

This repository contains personal Claude Code rules, conventions, and configurations that can be synced to other projects using the `dogma` plugin from:  
https://github.com/Marcel-Bich/marcel-bich-claude-marketplace

**Self-fulfilling repo:** This repository applies its own rules to itself.

## Usage

### Sync to a project

In any project with the dogma plugin installed:

```
/dogma:sync Marcel-Bich/marcel-bich-claude-dogma
```

### What gets synced

The sync process will interactively review:

- **Git configuration** (`gitconfig`) - User name, email for commits
- **Universal .gitignore** (`.gitignore`) - Comprehensive ignore patterns
- **Claude rules** (`CLAUDE.md`, `CLAUDE/*.md`) - Guidelines for Claude Code
- **Guides** (`GUIDES/*.md`) - Detailed conventions

## Structure

```
.
├── CLAUDE.md                       # Main entry point (always loaded)
├── CLAUDE/                         # Rule files (concise, ~5-10 lines each)
│   ├── CLAUDE.git.md               # Git rules, AI traces (critical via @)
│   ├── CLAUDE.honesty.md           # No hallucination guardrail (critical via @)
│   ├── CLAUDE.language.md          # Umlauts, German text rules (critical via @)
│   ├── CLAUDE.planning.md          # Complexity assessment, /create-plan (critical via @)
│   ├── CLAUDE.prompt-intervention.md # Skill suggestions, proactive help (critical via @)
│   ├── CLAUDE.prompt-injection.md  # Protection against malicious web content (critical via @)
│   ├── CLAUDE.security.md          # Dependencies, secrets, npm safety
│   ├── CLAUDE.environment.md       # .env handling, config management
│   ├── CLAUDE.legal.md             # Licensing, privacy, impressum
│   ├── CLAUDE.linting.md           # ESLint, official tools only
│   ├── CLAUDE.formatting.md        # Prettier, legacy project handling
│   ├── CLAUDE.build.md             # Vite, Vitest, pnpm
│   ├── CLAUDE.testing.md           # Test pyramid, E2E filtering
│   ├── CLAUDE.error-handling.md    # Logging, user messages
│   ├── CLAUDE.branching.md         # Git flow, PR workflow
│   ├── CLAUDE.code-review.md       # Review checklist
│   ├── CLAUDE.documentation.md     # Comments, README, JSDoc
│   ├── CLAUDE.versioning.md        # Semantic versioning
│   ├── CLAUDE.structure.md         # Dogma repo structure rules
│   ├── CLAUDE.naming.md            # Naming conventions
│   ├── CLAUDE.philosophy.md        # YAGNI, KISS, Rule of Three (critical via @)
│   └── CLAUDE.accessibility.md     # A11y + Mobile-First (optional)
├── GUIDES/                         # Detailed conventions
│   ├── git.md
│   ├── language.md
│   ├── planning.md
│   ├── prompt-intervention.md
│   ├── prompt-injection.md
│   ├── security.md
│   ├── environment.md
│   ├── legal.md
│   ├── linting.md
│   ├── formatting.md
│   ├── build.md
│   ├── testing.md
│   ├── error-handling.md
│   ├── branching.md
│   ├── code-review.md
│   ├── documentation.md
│   ├── versioning.md
│   ├── structure.md
│   ├── naming.md
│   ├── philosophy.md
│   └── accessibility.md
├── .claude/                        # Claude Code project settings
│   └── settings.json               # Permission allowlist (synced to projects)
├── .gitignore                      # Universal .gitignore (885 lines)
├── gitconfig                       # Git user configuration (demo data)
└── RECOMMENDATIONS.md              # Recommended plugins and MCPs
```

## Reference System

| Syntax | Meaning | Example |
|--------|---------|---------|
| `@file` | Critical, always load | `@CLAUDE/CLAUDE.git.md` |
| `` `file` `` | Situational, load when relevant | `` `CLAUDE/CLAUDE.versioning.md` `` |
| `For details see` | Optional, load if more context needed | `GUIDES/accessibility.md` |

## Topics Covered

| Category | Topics |
|----------|--------|
| **Critical** | Honesty, Git/AI traces, Language, Planning, Prompt Intervention, Prompt Injection Protection, Philosophy |
| **Security** | npm supply chain, socket.dev, snyk, secrets, dependency heuristics |
| **Legal** | MIT/Apache/GPL licensing, GDPR, Impressum (DE) |
| **Code Quality** | ESLint, Prettier, Vite, Vitest, Philosophy (YAGNI, KISS) |
| **Testing** | Test pyramid, E2E filtering, coverage |
| **Workflow** | Branching, PRs, code review, versioning |
| **Documentation** | Comments, README, JSDoc, CHANGELOG |
| **Recommendations** | Plugins (Safety Net, Signal), MCPs (context7, Playwright) |

## Related

- [marcel-bich-claude-marketplace](https://github.com/Marcel-Bich/marcel-bich-claude-marketplace) - Plugin marketplace containing the dogma plugin

## License

MIT License - see [LICENSE](LICENSE) for details.
