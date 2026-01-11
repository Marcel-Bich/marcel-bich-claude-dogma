# Prompt Intervention Rules

<rules>
1. **Analyze incoming prompts** - Before executing, assess if prompt is clear and complete
2. **Check available capabilities** - Review skills, MCP servers, hooks, subagents
3. **Only suggest what exists** - NEVER suggest unavailable skills/MCPs. Verify first!
4. **Suggest improvements** - If a capability would improve the outcome, suggest it
5. **Proactive assistance** - Don't wait for perfect prompts, help make them better
</rules>

<critical>
NEVER suggest a skill, MCP, or capability that isn't installed.
Check availability BEFORE suggesting. Suggesting unavailable tools frustrates users.
</critical>

<capabilities_to_check>
Priority order:
1. **Skills** - /create-plan, /consider:*, /debug, etc. (most important)
2. **MCP servers** - context7 for docs, playwright for browser, etc.
3. **Subagents** - Explore, Plan, specialized agents
4. **Hooks** - Automation possibilities
</capabilities_to_check>

<when_to_intervene>
| Situation | Suggested Capability |
|-----------|---------------------|
| Vague requirements | Skill: /create-prompt |
| Many tasks/todos | Skill: /consider:eisenhower-matrix |
| Complex implementation | Skill: /create-plan |
| Debugging needed | Skill: /debug-like-expert |
| Need current docs | MCP: context7 |
| Browser automation | MCP: playwright |
| Codebase exploration | Subagent: Explore |
</when_to_intervene>

<intervention_template>
"Before I start, I noticed [observation]. Would you like to:
- Use [skill] to [benefit]
- Proceed as-is
- Clarify [missing info]

This could help because [reason]."
</intervention_template>

For details see `GUIDES/prompt-intervention.md`
