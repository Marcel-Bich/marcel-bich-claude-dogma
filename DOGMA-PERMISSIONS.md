# Dogma Permissions

Configure what Claude is allowed to do autonomously.
Mark with `[x]` for auto, `[?]` for ask, `[ ]` for deny.

<permissions>
## Git Permissions
- [ ] May run `git add` autonomously
- [ ] May run `git commit` autonomously
- [ ] May run `git push` autonomously

## File Operations
- [ ] May delete files autonomously (rm, unlink, git clean)

## Workflow Permissions

Checkbox legend: `[ ]` = disabled, `[x]` = auto, `[?]` = on request

### Testing

When to run tests?
- [x] before commit
- [x] before push
- [x] on tasklist completion

What to test?
- [x] relevant tests
- [x] silent-failure check

### Review

When to review?
- [x] after implementation
- [x] before commit
- [x] before push

What to review?
- [x] changed code
- [ ] architecture
- [ ] types

### Fallback

When no tests exist:
- [x] spawn subagent for verification
- [ ] skip

### Hydra

Parallel work (only if Hydra available, otherwise sequential):
- [x] use Hydra for 2+ independent tasks

### TDD

Test-Driven Development:
- [x] TDD when tests exist
- [ ] enforce TDD even without existing tests

### Final Verification

After merge/review (order: relevant tests -> build -> ALL tests):
- [x] run relevant tests
- [x] check build
- [x] run ALL tests
</permissions>

## Behavior

| Permission | [x] auto | [?] ask | [ ] deny |
|------------|----------|---------|----------|
| git add | Stages files | Asks first | Blocked |
| git commit | Creates commits | Asks first | Blocked |
| git push | Pushes to remote | Asks first | Blocked |
| delete files | Deletes files | Asks first | Logged to TO-DELETE.md |

## Subagent Delegation
- [x] Skill tool usage counts as delegation
