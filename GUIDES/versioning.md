# Versioning Guide

<semantic_versioning>
Format: `major.minor.patch`

| Type | When | Example |
|------|------|---------|
| **major** | Groundbreaking changes, relaunch, full rewrite, heavy migration needed | 1.2.0 -> 2.0.0 |
| **minor** | Breaking changes, migration required, BIG new features that significantly change the product | 1.1.3 -> 1.2.0 |
| **patch** | Everything else: bugfixes, small features, improvements, refactoring, small additions | 1.1.2 -> 1.1.3 |

**Default to patch!** Most changes are patch. When in doubt, use patch.
</semantic_versioning>

<decision_guide>
Ask yourself:
1. Does this require users to migrate/change their code? -> **minor** (or major if heavy)
2. Is this a BIG feature that fundamentally changes what the product does? -> **minor**
3. Everything else? -> **patch**

Small new features, minor additions, quality improvements = **patch**
</decision_guide>

<common_mistakes>
| Mistake | Consequence |
|---------|-------------|
| Version changed in only one file | Inconsistency, build errors |
| Small feature bumped to minor | Version inflation, loses meaning |
| Breaking change as patch | User code breaks unexpectedly |
| No commit prefix | History hard to follow |
</common_mistakes>

<release_checklist>
1. **Identify all version files** - Which files contain versions?
2. **Update all files** - Do NOT forget any!
3. **Commit prefix** - `vX.Y.Z:` at the start of commit message
4. **Create tag** (optional) - `git tag vX.Y.Z`
</release_checklist>

<version_files>
Applies to ALL project types:

| Project Type | Typical Version Files |
|--------------|----------------------|
| **Claude Code Plugin** | `plugin.json`, `marketplace.json` |
| **MCP Server** | `package.json`, `mcp.json` |
| **NPM Package** | `package.json`, `package-lock.json` |
| **Python Package** | `pyproject.toml`, `setup.py`, `__version__.py` |
| **Go Module** | `go.mod`, Git Tags |
| **Rust Crate** | `Cargo.toml` |
| **Flutter/Dart** | `pubspec.yaml` |
| **Other** | README, CHANGELOG, manifest files |
</version_files>

<workflow_example>
```bash
# 1. Made changes (bugfix)
# 2. Bump version in ALL relevant files: 1.1.2 -> 1.1.3
# 3. Commit
git commit -m "v1.1.3: Fix timeout issue in API calls"

# 4. Optional: Tag
git tag v1.1.3

# 5. Push
git push && git push --tags
```
</workflow_example>
