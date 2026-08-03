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
Subagents only modify files - they NEVER git add/commit/push. The main agent does
add + commit + push after review, so the shared working-tree index has one owner
(parallel subagents would race `.git/index.lock`).
(No `@`-import here - file is already loaded via `CLAUDE.md` Section 2.)
</git_rules_reference>

<decision_flow>
Before EVERY action, ask:
1. Does this require user interaction? → Main agent handles
2. Is there a specialized agent for this? → Use it
3. No specialized agent? → Use general-purpose subagent

NEVER do directly what a subagent could do.
</decision_flow>

<available_agents>
Agent names vary per install - a rule set that ships everywhere cannot hardcode a
reliable list. Before naming a specialized agent, confirm it is actually listed in
YOUR environment; never assume a specific one exists, or you get "agent type not
found". If it is not listed, fall back to a built-in.

**Built-in (always available):**
- Explore - Codebase exploration
- Plan - Planning and strategy
- general-purpose - Fallback for any unspecialized task

**Specialized (only if an installed plugin provides them):** discover them from
what your environment actually lists at runtime (e.g. reviewers, auditors,
validators) - do not rely on fixed names.
</available_agents>

<hydra_usage>
When to use Hydra:
- 2+ tasks that are independent (no shared state)
- Tasks can run in parallel without conflicts
- Each task can be isolated in its own worktree

Commands: `/hydra:create`, `/hydra:spawn`, `/hydra:parallel`
</hydra_usage>

For details see `GUIDES/subagents.md`
