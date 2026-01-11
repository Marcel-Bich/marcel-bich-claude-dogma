# Planning Guide

<why_planning>
## Why Planning Matters

Complex tasks without planning lead to:
- Rework when requirements become clearer
- Missed steps discovered late
- Inconsistent architecture decisions
- Wasted time on wrong approaches
- User frustration from back-and-forth

Planning upfront costs 5 minutes, saves hours of fixes.
</why_planning>

<complexity_assessment>
## Assessing Complexity

**Simple tasks (no planning needed):**
- Single file change
- Clear, specific requirement
- Obvious implementation
- No dependencies

**Complex tasks (planning recommended):**
- 3+ files affected
- "Build a feature that..."
- "Refactor the..."
- "Set up infrastructure for..."
- Unclear scope or requirements
- Multiple valid solutions

**Ask yourself:** "If I start now, will I need to undo work later?"
</complexity_assessment>

<create_plan_benefits>
## Benefits of /create-plan (taches-cc-resources)

If the user has taches-cc-resources installed, /create-plan provides:

1. **Structured hierarchy** - Brief → Roadmap → Phase plans
2. **Verification criteria** - Clear definition of done
3. **Context preservation** - Handoff documents for long tasks
4. **Progress tracking** - Built-in status updates
5. **Scope management** - Prevents scope creep

**When to suggest:**
- New project setup
- Multi-phase implementations
- Architectural changes
- Features spanning multiple sessions
</create_plan_benefits>

<plan_file_structure>
## Manual Plan File Structure

If not using /create-plan, a simple PLAN.md:

```markdown
# Task: [Brief description]

## Goal
What we're trying to achieve.

## Steps
1. [ ] Step one
2. [ ] Step two
3. [ ] Step three

## Open Questions
- Question needing clarification

## Progress
- [x] Completed item
- [ ] Pending item
```
</plan_file_structure>

<when_not_to_plan>
## When NOT to Suggest Planning

- User explicitly says "just do it"
- Task is clearly simple
- User is in a hurry (but warn about risks)
- Follow-up to already planned work
- Bug fixes with obvious solutions
</when_not_to_plan>
