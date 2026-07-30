# Subagent Rules

<rules>
1. **Main agent = delegation only** - Main agent handles ONLY user interaction, orchestration, and delegation
2. **Everything else = subagent** - Any task without user interaction MUST go to a subagent
3. **Check agents first** - Before EVERY action, check if a specialized agent exists
4. **No fitting agent? Use general-purpose** - Never do work directly that a subagent could handle
5. **Hydra for parallel work** - 2+ independent tasks → Hydra MUST be used
6. **TDD is mandatory** - If project has tests → write test first, then implementation
</rules>

<git_rules_reference>
Git-related rules (gitignore, commits, AI attribution) live in `CLAUDE/CLAUDE.git.md`.
Subagents MUST respect them just like the main agent.
(No `@`-import here - file is already loaded via `CLAUDE.md` Section 2.)

Subagents only modify files - they never git add/commit/push; the main agent does add+commit+push after review.
</git_rules_reference>

<decision_flow>
Before EVERY action, ask:
1. Does this require user interaction? → Main agent handles
2. Is there a specialized agent for this? → Use it
3. No specialized agent? → Use general-purpose subagent

NEVER do directly what a subagent could do.
</decision_flow>

<available_agents>
**Guaranteed built-ins (always available):**
- Explore - Codebase exploration and file search
- Plan - Planning and strategy
- general-purpose - Fallback for unspecialized tasks

**Specialized agents:**
Do NOT assume any specific specialized agent (e.g. code-reviewer, plugin-validator, skill-auditor) exists. A specialized agent is available ONLY if an installed plugin provides it. Discover what actually exists at runtime from the environment's own agent listing, and confirm an agent is listed before spawning it. If a needed specialized agent is not listed, fall back to general-purpose. Never spawn a fixed agent name on the assumption that it is installed - that causes "agent type not found".
</available_agents>

<hydra_usage>
When to use Hydra:
- 2+ tasks that are independent (no shared state)
- Tasks can run in parallel without conflicts
- Each task can be isolated in its own worktree

Commands: `/hydra:create`, `/hydra:spawn`, `/hydra:parallel`
</hydra_usage>

For details see `GUIDES/subagents.md`
