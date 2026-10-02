# Dogma Permissions

Configure what Claude is allowed to do autonomously.
Mark with `[x]` for auto, `[?]` for ask, `[ ]` for deny.

<permissions>
## Git Permissions
- [x] (§6gpt) May run `git add` autonomously
- [x] (§2w1t) May run `git commit` autonomously
- [?] (§bww9) May run `git push` autonomously
- Subagents: only modify files, NEVER git add/commit/push. Only the main agent adds+commits+pushes after review (the shared working-tree index has one owner; parallel subagents would race `.git/index.lock`). Exception: in its OWN git worktree a subagent has its own index and may commit on its worktree branch - never push or merge; push, merge and release stay with the main agent.

## File Operations
- [ ] (§0lgy) May delete files autonomously (rm, unlink, git clean)

## Workflow Permissions

Checkbox legend: `[ ]` = disabled, `[x]` = auto, `[?]` = on request

### Testing

When to run tests?
- [x] (§pq4z) before commit
- [x] (§zn2t) before push
- [x] (§r308) on tasklist completion

What to test?
- [x] (§em4i) relevant tests
- [x] (§2t40) silent-failure check

### Review

When to review?
- [x] (§d33m) after implementation
- [x] (§38bw) before commit
- [x] (§hms3) before push

What to review?
- [x] (§z66u) changed code
- [ ] (§6h8w) architecture
- [ ] (§n0wg) types

### Fallback

When no tests exist:
- [x] (§33tc) spawn subagent for verification
- [ ] (§ab7k) skip

### Hydra

Parallel work (only if Hydra available, otherwise sequential):
- [x] (§xw1i) use Hydra for 2+ independent tasks

Worktree cleanup at item close ([x] = remove without asking, [?] = ask each time, [ ] = never):
- [x] (§36ch) clean up merged worktrees automatically

Worktree files: without a "Worktree files (§47p9)" list, new worktrees link CLAUDE.md, CLAUDE/, GUIDES/,
DOGMA-PERMISSIONS.md and everything unversioned under .credo/ (see the dogma docs to override).

### Subagent Delegation

What counts as delegation (prevents subagent-first warning):
- [x] (§o85w) Task tool usage counts as delegation
- [x] (§i397) Skill tool usage counts as delegation

### TDD

Test-Driven Development:
- [x] (§on8g) TDD when tests exist
- [ ] (§7i3k) enforce TDD even without existing tests

### Final Verification

After merge/review (order: relevant tests -> build -> ALL tests):
- [x] (§0c7y) run relevant tests
- [x] (§aq02) check build
- [x] (§3dy3) run ALL tests
- [ ] (§8eyz) run ALL tests only at release (release = the commit that bundles several items with the version bump; never a tag)
</permissions>

## Behavior

| Permission | [x] auto | [?] ask | [ ] deny |
|------------|----------|---------|----------|
| git add | Stages files | Asks first | Blocked |
| git commit | Creates commits | Asks first | Blocked |
| git push | Pushes to remote | Asks first | Blocked |
| delete files | Deletes files | Asks first | Logged to TO-DELETE.md |
