# Code Review Guide

<reviewer_checklist>
## Reviewer Checklist

**Functionality:**
- [ ] Does it do what it's supposed to?
- [ ] Edge cases handled?
- [ ] Error handling appropriate?

**Code Quality:**
- [ ] Code is readable and understandable?
- [ ] No unnecessary complexity?
- [ ] Follows project conventions?

**Testing:**
- [ ] Tests exist for new functionality?
- [ ] Tests pass?
- [ ] Edge cases tested?

**Security:**
- [ ] No hardcoded secrets?
- [ ] Input validated?
- [ ] No injection vulnerabilities?
- [ ] Auth/authz checked?

**Performance:**
- [ ] No obvious performance issues?
- [ ] No unnecessary loops/queries?
</reviewer_checklist>

<feedback_style>
## Giving Feedback

**Good feedback:**
```markdown
Consider using `Array.map()` here instead of the for loop -
it would make the intent clearer:

const names = users.map(u => u.name);
```

**Bad feedback:**
```markdown
This is wrong.
```

**Principles:**
- Suggest, don't command
- Explain the "why"
- Offer alternatives
- Be kind
</feedback_style>

<pr_size>
## PR Size Guidelines

| Lines Changed | Rating | Action |
|---------------|--------|--------|
| < 100 | Excellent | Easy to review |
| 100-400 | Good | Reasonable |
| 400-800 | Large | Consider splitting |
| > 800 | Too large | Split into smaller PRs |

**Exception:** Generated code, migrations, or formatting commits.

**How to split large PRs:**
1. Extract refactoring into separate PR
2. Split by feature/component
3. Create "Part 1/2/3" PRs if sequential
</pr_size>

<self_review>
## Solo Developer: Self-Review

Even without a team, review your own code:

1. **Wait before merging** - Come back after a break
2. **Read the diff** - View changes as reviewer would
3. **Run the checklist** - Go through items above
4. **Test manually** - Click through the feature

**Command for self-review:**
```bash
# Review all changes before commit
git diff --staged

# Review what will be in PR
git diff main..HEAD
```
</self_review>

<common_issues>
## Common Issues to Watch For

| Issue | Example | Solution |
|-------|---------|----------|
| Magic numbers | `if (count > 7)` | Use named constant |
| Long functions | 100+ line function | Split into smaller functions |
| Deep nesting | 4+ levels of if/for | Early returns, extract methods |
| Copy-paste code | Same logic twice | Extract to function |
| No error handling | Uncaught promises | Add try/catch |
| Console.log left in | Debug statements | Remove before merge |
</common_issues>

<approve_decline>
## When to Approve/Decline

**Approve when:**
- All checklist items pass
- Tests pass
- No blocking issues
- Minor suggestions can be addressed later

**Request changes when:**
- Tests fail or missing
- Security issues
- Breaking changes not documented
- Significant design concerns

**Comment (not approve/decline) when:**
- Questions need answering
- Suggestions that don't block merge
</approve_decline>
