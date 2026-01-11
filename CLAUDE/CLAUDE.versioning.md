# Version Management Rules

<rules>
1. Always use semantic versioning (major.minor.patch)
2. Update ALL version files before release - never forget any
3. Use commit prefix `vX.Y.Z:` for version bumps
4. **Default to patch** - most changes are patch, not minor!
</rules>

<version_levels>
| Level | When to use |
|-------|-------------|
| **major** | Groundbreaking changes, relaunch, full rewrite, heavy migration needed |
| **minor** | Breaking changes, migration required, BIG new features (not small ones!) |
| **patch** | Everything else: bugfixes, small features, improvements, refactoring |
</version_levels>

<critical>
Small new features = PATCH, not minor!
Only BIG features that significantly change the product = minor.
When in doubt, use patch.
</critical>

For details see `GUIDES/versioning.md`
