# Branching Guide

<branch_naming>
## Branch Naming

| Prefix | Use for | Example |
|--------|---------|---------|
| `feature/` | New features | `feature/user-authentication` |
| `fix/` | Bug fixes | `fix/login-timeout` |
| `chore/` | Maintenance | `chore/update-dependencies` |
| `docs/` | Documentation | `docs/api-readme` |
| `refactor/` | Code refactoring | `refactor/user-service` |

**Format:** `prefix/short-description`
- Lowercase
- Hyphens between words
- No special characters
</branch_naming>

<workflow>
## Simple Git Flow

```
main ─────────────────────────────────────
       \                    /
        feature/new-thing ──
```

**For most projects:**
1. Branch from `main`
2. Work on feature
3. Create PR
4. Merge to `main`
5. Delete branch

**For larger teams (optional develop branch):**
```
main ─────────────────────────────────────
       \                    /
develop ────────────────────
         \        /
          feature ─
```
</workflow>

<commands>
## Common Commands

```bash
# Start new feature
git checkout main
git pull
git checkout -b feature/my-feature

# Work on feature
git add .
git commit -m "Add user login form"

# Push and create PR
git push -u origin feature/my-feature
# Then create PR on GitHub/GitLab

# After PR is merged
git checkout main
git pull
git branch -d feature/my-feature  # Delete local
```
</commands>

<merge_strategies>
## Merge Strategies

| Strategy | When | Command |
|----------|------|---------|
| **Merge commit** | Default, preserves history | `git merge feature` |
| **Squash** | Clean history, many small commits | `git merge --squash feature` |
| **Rebase** | Linear history (advanced) | `git rebase main` |

**Recommendation:** Use squash merge for feature branches via PR.
</merge_strategies>

<conflict_resolution>
## Handling Conflicts

```bash
# Update your branch with latest main
git checkout feature/my-feature
git fetch origin
git rebase origin/main

# If conflicts occur:
# 1. Edit conflicted files
# 2. git add <resolved-files>
# 3. git rebase --continue

# Force push after rebase
git push --force-with-lease
```

**Prevention:**
- Keep branches short-lived (max few days)
- Merge main into feature frequently
- Communicate with team about overlapping work
</conflict_resolution>

<protected_branches>
## Branch Protection (Recommended)

**Settings for `main`:**
- [ ] Require pull request reviews
- [ ] Require status checks (CI)
- [ ] Require branches to be up to date
- [ ] No direct pushes

Configure in: GitHub Settings > Branches > Branch protection rules
</protected_branches>

<solo_developer>
## Solo Developer Workflow

**Even solo, use branches:**
```bash
# Feature work
git checkout -b feature/new-thing
# ... work ...
git commit -m "Add new thing"
git checkout main
git merge feature/new-thing
git branch -d feature/new-thing
git push
```

**Benefits:**
- Easy to abandon incomplete work
- Can switch context quickly
- History shows feature boundaries
</solo_developer>
