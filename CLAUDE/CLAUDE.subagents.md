# Subagent Rules

<rules>
1. **Main agent = delegation only** - Main agent handles ONLY user interaction, orchestration, and delegation
2. **Everything else = subagent** - Any task without user interaction MUST go to a subagent
3. **Check agents first** - Before EVERY action, check if a specialized agent exists
4. **No fitting agent? Use general-purpose** - Never do work directly that a subagent could handle
5. **Hydra for parallel work** - 2+ independent tasks → Hydra MUST be used
6. **TDD is mandatory** - If project has tests → write test first, then implementation
</rules>

<decision_flow>
Before EVERY action, ask:
1. Does this require user interaction? → Main agent handles
2. Is there a specialized agent for this? → Use it
3. No specialized agent? → Use general-purpose subagent

NEVER do directly what a subagent could do.
</decision_flow>

<available_agents>
**Code Analysis:**
- code-reviewer - Review code quality and patterns
- code-architect - Analyze architecture decisions
- code-explorer - Navigate and understand codebases
- silent-failure-hunter - Find hidden error paths

**Development:**
- agent-creator - Create new subagents
- plugin-validator - Validate plugin structure
- skill-reviewer - Review skill implementations

**Auditing:**
- skill-auditor - Audit skill files
- slash-command-auditor - Audit slash commands
- subagent-auditor - Audit subagent configurations

**Built-in:**
- Explore - Codebase exploration
- Plan - Planning and strategy
- general-purpose - Fallback for unspecialized tasks
</available_agents>

<hydra_usage>
When to use Hydra:
- 2+ tasks that are independent (no shared state)
- Tasks can run in parallel without conflicts
- Each task can be isolated in its own worktree

Commands: `/hydra:create`, `/hydra:spawn`, `/hydra:parallel`
</hydra_usage>

GUIDES/subagents.md
