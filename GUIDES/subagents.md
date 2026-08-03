# Subagent Selection Guide

Guide for selecting and orchestrating subagents.

---

## Why Subagent-First

<section name="philosophy">
The Main Agent is an orchestrator, not an executor. This separation has several advantages:

**Focus**: The Main Agent focuses on analysis, planning, and coordination. Subagents handle the actual work.

**Isolation**: Subagents work in isolated contexts. Errors in one agent do not affect others.

**Specialization**: Each agent has optimized prompts for its task. A reviewing agent reviews differently than a testing agent.

**Parallelization**: Independent tasks can be processed simultaneously by different agents.

**Traceability**: Clear responsibilities make decisions transparent.
</section>

---

## Agent Selection Decision Tree

<section name="decision_tree">
Before EVERY action, go through these questions:

```
1. Does the action require user interaction?
   |-- YES -> Main Agent keeps the task
   +-- NO -> continue to 2

2. Is there a specialized agent for this task?
   |-- YES -> Use that agent
   +-- NO -> continue to 3

3. Is the task complex enough for delegation?
   |-- YES -> general-purpose agent
   +-- NO -> Main Agent handles it directly
```

**Examples of user interaction:**
- Clarifying requirements
- Confirming destructive actions
- Choosing between options
- Presenting results

**No user interaction needed:**
- Code analysis
- File exploration
- Test execution
- Lint checks
</section>

---

## Available Agents by Category

### Code Analysis & Review

<section name="code_analysis_agents">
| Agent | Source | Use For |
|-------|--------|---------|
| code-reviewer | feature-dev, pr-review-toolkit, superpowers | Reviewing code changes, quality checks |
| code-architect | feature-dev | Designing feature architecture |
| code-explorer | feature-dev | Exploring and understanding codebases |
| code-simplifier | pr-review-toolkit | Simplifying complex code |
| silent-failure-hunter | pr-review-toolkit | Finding silent errors and missing error handling |
| type-design-analyzer | pr-review-toolkit | Analyzing TypeScript type design |
</section>

### Development & Creation

<section name="development_agents">
| Agent | Source | Use For |
|-------|--------|---------|
| agent-creator | plugin-dev | Creating new agents |
| plugin-validator | plugin-dev | Validating plugins |
| skill-reviewer | plugin-dev | Reviewing skills |
</section>

### Auditing

<section name="auditing_agents">
| Agent | Source | Use For |
|-------|--------|---------|
| skill-auditor | taches-cc-resources | Auditing skills for best practices |
| slash-command-auditor | taches-cc-resources | Auditing slash commands |
| subagent-auditor | taches-cc-resources | Auditing subagent configurations |
</section>

### Analysis

<section name="analysis_agents">
| Agent | Source | Use For |
|-------|--------|---------|
| comment-analyzer | pr-review-toolkit | Analyzing PR comments |
| pr-test-analyzer | pr-review-toolkit | Analyzing tests in PRs |
| conversation-analyzer | hookify | Analyzing conversations |
</section>

### Built-in

<section name="builtin_agents">
| Agent | Source | Use For |
|-------|--------|---------|
| Explore | built-in | Codebase exploration, file search |
| Plan | built-in | Planning tasks |
| general-purpose | built-in | Everything else without user interaction |

**Note**: Only the built-in agents (Explore, Plan, general-purpose) are guaranteed. Every other agent named in this guide is an EXAMPLE from a specific plugin and exists only if that plugin is installed - names vary per install. Always confirm an agent is actually listed in your environment before spawning it (otherwise you get "agent type not found"); if it is not there, fall back to a built-in. Treat the tables and quick-reference below as examples, not a guaranteed roster.
</section>

---

## Orchestration Flow

<section name="orchestration_flow">
The complete flow for complex tasks:

```
1. Receive user prompt
   +-- Main Agent analyzes the request

2. Check context
   |-- Tests present? -> Activate TDD workflow
   |-- Multiple independent tasks? -> Use Hydra
   +-- Specialized agents needed? -> Identify them

3. Delegate to subagents
   |-- Spawn matching agents for each task
   +-- IMPORTANT: Inform subagents to respect .gitignore

4. Collect feedback
   +-- Gather results from subagents

5. Spawn review agents
   |-- code-reviewer for changes
   |-- silent-failure-hunter for error handling
   +-- type-design-analyzer for TypeScript

6. Corrections via subagents
   +-- Fix discovered issues

7. Run /dogma:lint
   +-- Ensure formatting and linting

8. Final review
   +-- Last quality check

9. Inform user
   +-- Present results, answer questions
```
</section>

---

## Hydra Rule

<section name="hydra_rule">
**Rule**: When 2 or more independent tasks exist, Hydra MUST be used.

**Independent tasks** are tasks that:
- Do not edit shared files
- Have no sequential dependencies
- Can be executed in parallel

**Example independent:**
- Task A: Write tests for module X
- Task B: Create documentation for module Y
- Task C: Fix linting errors in module Z

**Example dependent:**
- Task A: Define interface
- Task B: Implement interface (needs A)
- Task C: Tests for implementation (needs B)

**Hydra commands:**
```bash
/hydra:create    # Create worktree
/hydra:spawn     # Start agent in worktree
/hydra:parallel  # Start multiple agents in parallel
/hydra:status    # Check status
/hydra:merge     # Merge results
```
</section>

---

## TDD Rule

<section name="tdd_rule">
**Rule**: When tests exist in the project, TDD is MANDATORY.

**Checking if tests exist:**
- `__tests__/` directory present?
- `*.test.ts`, `*.spec.ts` files present?
- `vitest.config.*` or `jest.config.*` present?
- `test` script in `package.json`?

If at least one applies: TDD is active.

**TDD workflow:**
1. Write a failing test
2. Minimal implementation that makes the test pass
3. Refactoring
4. Repeat

**Benefits:**
- Specification before implementation
- Regression protection
- Clean API design
- Confidence in changes

**Exceptions:**
- Pure configuration files
- Documentation
- Exploratory prototypes (with user confirmation)
</section>

---

## Quick Reference

<section name="quick_reference">
```
Task                       -> Agent
-----------------------------------------
Review code                -> code-reviewer
Plan architecture          -> code-architect
Explore codebase           -> Explore / code-explorer
Simplify code              -> code-simplifier
Find errors                -> silent-failure-hunter
Analyze types              -> type-design-analyzer
Create agent               -> agent-creator
Validate plugin            -> plugin-validator
Review skill               -> skill-reviewer
Audit skill                -> skill-auditor
Audit slash command         -> slash-command-auditor
Audit subagent             -> subagent-auditor
Analyze PR comments        -> comment-analyzer
Analyze PR tests           -> pr-test-analyzer
Analyze conversation       -> conversation-analyzer
Planning                   -> Plan
Other (without user)       -> general-purpose
```
</section>
