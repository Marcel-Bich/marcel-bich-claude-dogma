# Claude Code Guidelines

<MANDATORY_RULES>
## MANDATORY - ALWAYS FOLLOW WITHOUT EXCEPTION

These rules apply ALWAYS, without exception, for EVERY action:

### 1. Subagent-First (HIGHEST PRIORITY)
@CLAUDE/CLAUDE.subagents.md

**BEFORE EVERY ACTION check:**
- Does this require user interaction? -> Main Agent OK
- Is there a specialized agent for this? -> USE IT!
- No fitting agent? -> general-purpose subagent
- 2+ independent tasks? -> Hydra MANDATORY

**NEVER work directly when a subagent exists.**

### 2. Git Rules (NO EXCEPTIONS)
@CLAUDE/CLAUDE.git.md

**ALWAYS:**
- No AI attribution (Co-Authored-By, "Generated with Claude")
- No AI traces (curly quotes, em-dashes, emojis in code)
- Never delete local files without explicit user confirmation

</MANDATORY_RULES>

---

## Other Important Rules

@CLAUDE/CLAUDE.honesty.md
@CLAUDE/CLAUDE.language.md
@CLAUDE/CLAUDE.planning.md
@CLAUDE/CLAUDE.prompt-intervention.md
@CLAUDE/CLAUDE.prompt-injection.md
@CLAUDE/CLAUDE.philosophy.md

---

<situational_rules>
Read these files only when relevant:

**Project Setup:**
- `CLAUDE/CLAUDE.naming.md` - when naming projects, repos, or packages
- `CLAUDE/CLAUDE.structure.md` - when modifying repo structure or adding files
- `CLAUDE/CLAUDE.environment.md` - when setting up .env or config

**Security & Legal:**
- `CLAUDE/CLAUDE.security.md` - when adding dependencies or handling secrets
- `CLAUDE/CLAUDE.legal.md` - when adding LICENSE, privacy policy, or impressum

**Code Quality:**
- `CLAUDE/CLAUDE.linting.md` - when setting up or configuring ESLint
- `CLAUDE/CLAUDE.formatting.md` - when setting up or using Prettier
- `CLAUDE/CLAUDE.build.md` - when setting up Vite, Vitest, or build tools
- `CLAUDE/CLAUDE.testing.md` - when writing or running tests
- `CLAUDE/CLAUDE.error-handling.md` - when implementing error handling or logging

**Workflow:**
- `CLAUDE/CLAUDE.versioning.md` - when bumping versions or releasing
- `CLAUDE/CLAUDE.branching.md` - when creating branches or PRs
- `CLAUDE/CLAUDE.code-review.md` - when reviewing code
- `CLAUDE/CLAUDE.documentation.md` - when writing docs or comments

**Optional (end-user apps only):**
- `CLAUDE/CLAUDE.accessibility.md` - when building user-facing web UI
</situational_rules>
