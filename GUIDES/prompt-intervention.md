# Prompt Intervention Guide

<philosophy>
## Philosophy

Users don't always know the best way to prompt. As an agent with knowledge of available tools, you can:
- Recognize when a skill would help
- Suggest better approaches
- Save the user time and effort
- Improve output quality

This is proactive assistance, not gatekeeping.
</philosophy>

<capabilities_overview>
## Available Capabilities

Check these in priority order:

### 1. Skills (Most Important)
Slash commands that extend functionality:
- `/create-plan`, `/run-plan` - Structured planning
- `/consider:*` - Mental models (eisenhower, pareto, swot, etc.)
- `/debug`, `/debug-like-expert` - Systematic debugging
- `/create-prompt` - Prompt engineering
- `/audit-*` - Code review and auditing

### 2. MCP Servers
External tools via Model Context Protocol:
- **context7** - Current documentation lookup (avoids hallucination)
- **playwright** - Browser automation and testing
- **Custom MCPs** - Project-specific tools

### 3. Subagents
Specialized agents for delegation:
- **Explore** - Fast codebase exploration
- **Plan** - Architecture planning
- **Bash** - Command execution

### 4. Hooks
Automation on events:
- PreToolUse, PostToolUse
- Can suggest setting up automation for repetitive tasks
</capabilities_overview>

<skill_mapping>
## Skill Mapping by Situation

### Unclear Requirements
| Signal | Skill | Why |
|--------|-------|-----|
| "Build something that..." | /create-prompt | Clarify requirements first |
| Missing acceptance criteria | /create-plan | Define success criteria |
| Vague scope | Ask clarifying questions | Before suggesting skills |

### Prioritization Needed
| Signal | Skill | Why |
|--------|-------|-----|
| Multiple todos/tasks | /consider:eisenhower-matrix | Prioritize by urgency/importance |
| "What should I do first?" | /consider:pareto | Focus on 20% that gives 80% |
| Competing features | /consider:opportunity-cost | Understand tradeoffs |

### Complex Implementation
| Signal | Skill | Why |
|--------|-------|-----|
| Multi-step task | /create-plan | Structured approach |
| Architecture decision | /consider:first-principles | Break down fundamentals |
| "How should I structure..." | /consider:monolith vs modular | Right architecture |

### Problem Solving
| Signal | Skill | Why |
|--------|-------|-----|
| Bug not found easily | /debug-like-expert | Systematic investigation |
| "Why isn't this working?" | /consider:5-whys | Root cause analysis |
| Performance issues | /consider:pareto | Find bottlenecks |

### Decision Making
| Signal | Skill | Why |
|--------|-------|-----|
| "Should I use X or Y?" | /consider:swot | Compare options |
| Long-term vs short-term | /consider:10-10-10 | Time horizon analysis |
| Overthinking | /consider:occams-razor | Simplest solution |
</skill_mapping>

<mcp_mapping>
## MCP Server Mapping

| Situation | MCP | Why |
|-----------|-----|-----|
| Need current API docs | context7 | Avoids outdated/hallucinated info |
| "How does X library work?" | context7 | Get actual documentation |
| Browser testing needed | playwright | Automate browser interactions |
| Visual verification | playwright | Screenshot comparisons |
| Web scraping task | playwright | Navigate and extract data |
</mcp_mapping>

<subagent_mapping>
## Subagent Mapping

| Situation | Subagent | Why |
|-----------|----------|-----|
| "Where is X in the codebase?" | Explore | Fast file/pattern search |
| Need architecture overview | Explore | Codebase understanding |
| Complex planning needed | Plan | Structured approach |
| Many commands to run | Bash (background) | Parallel execution |
</subagent_mapping>

<intervention_examples>
## Intervention Examples

**Vague prompt:**
```
User: "Make the app better"

Agent: "Before I start, 'better' could mean many things. Would you like to:
- Use /create-prompt to clarify what 'better' means (performance? UX? features?)
- Tell me specific areas to improve
- Let me analyze the codebase first and suggest improvements"
```

**Overwhelmed user:**
```
User: "I have so many things to do, where do I start?"

Agent: "I can help prioritize. Would you like to:
- Use /consider:eisenhower-matrix to categorize by urgency/importance
- Use /check-todos to review outstanding items
- Tell me your top 5 tasks and I'll help prioritize"
```

**Complex task:**
```
User: "Refactor the authentication system"

Agent: "This is a significant change affecting security. Would you like to:
- Use /create-plan to structure this properly (recommended)
- Discuss the approach before implementation
- Proceed with my best judgment (riskier)"
```
</intervention_examples>

<when_not_to_intervene>
## When NOT to Intervene

- User gives clear, specific instructions
- User says "just do it" or similar
- Follow-up to previous discussion (context already established)
- Simple, obvious tasks
- User is clearly experienced and knows what they want

**Rule:** Intervene to help, not to slow down.
</when_not_to_intervene>

<available_skills_check>
## Checking Available Capabilities

CRITICAL: Only suggest what's actually available!

### How to Check

**Skills:**
- Look at Skill tool description in system prompt
- Check "Available skills:" section
- If not listed, DON'T suggest it

**MCP Servers:**
- Look for `mcp__*` tools in available tools
- `mcp__context7__*` = context7 available
- `mcp__playwright__*` = playwright available
- If no mcp tools, DON'T suggest MCPs

**Subagents:**
- Check Task tool description for available agent types
- Only suggest listed subagent_types

### Examples

```
# WRONG - suggesting without checking
"You should use /create-plan for this"
(But taches-cc-resources isn't installed!)

# RIGHT - checking first
"I see taches-cc-resources is available. Would you like to use /create-plan?"

# RIGHT - when not available
"This task is complex. Would you like me to create a simple PLAN.md to track progress?"
(Offering alternative when skill isn't available)
```

### Fallbacks When Not Available

| Missing | Fallback |
|---------|----------|
| /create-plan | Offer to create simple PLAN.md manually |
| context7 MCP | Use WebSearch or WebFetch |
| /consider:* | Apply the mental model yourself in response |
| playwright MCP | Describe manual testing steps |
</available_skills_check>
