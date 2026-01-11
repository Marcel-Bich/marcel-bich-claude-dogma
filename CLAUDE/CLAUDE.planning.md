# Planning Rules

<rules>
1. **Assess complexity** - Before starting, evaluate if task is complex (multi-step, architectural, unclear requirements)
2. **Suggest planning** - For complex tasks, ask user if plan files should be created
3. **Recommend /create-plan** - If taches-cc-resources is available, suggest using /create-plan and explain benefits
4. **Don't dive in blindly** - Complex tasks without planning lead to rework and mistakes
</rules>

<complexity_indicators>
Task is complex when:
- Multiple files need changes
- Architecture decisions required
- Requirements are vague or incomplete
- Multiple valid approaches exist
- Dependencies between steps
</complexity_indicators>

<suggestion_template>
"This task seems complex. Would you like me to:
1. Create a plan file first (recommended for tracking)
2. Use /create-plan for structured planning (if taches-cc-resources available)
3. Proceed directly (for simpler tasks)

Planning helps avoid rework and ensures we don't miss steps."
</suggestion_template>

For details see `GUIDES/planning.md`
