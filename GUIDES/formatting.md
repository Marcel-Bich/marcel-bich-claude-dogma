# Formatting Guide

<tool_selection>
## Recommended Stack

| Tool | Purpose |
|------|---------|
| **Prettier** | Code formatting (JS, TS, CSS, JSON, MD, etc.) |
| **EditorConfig** | Basic editor settings (indent, line endings) |

**Why Prettier:**
- Opinionated = no debates about style
- Wide language support
- Integrates with all major editors
- Works with ESLint
</tool_selection>

<legacy_project_handling>
## Legacy Projects - CRITICAL

**Problem:** Running Prettier on legacy code causes massive diffs that:
- Make git history hard to read
- Create merge conflicts
- Hide actual changes in noise

**Solution: Format only what you change**

```bash
# Format only staged files (recommended for legacy)
pnpm prettier --write $(git diff --staged --name-only)

# Format only specific files
pnpm prettier --write src/components/Button.tsx

# Check without writing
pnpm format:check
```

**Before formatting entire project, ASK USER:**
- "This project has unformatted code. Format all files? This will cause large diffs."
- If yes: Create dedicated formatting commit first
- If no: Only format files you modify
</legacy_project_handling>

<configuration>
## Prettier Configuration

```json
// .prettierrc
{
  "semi": true,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5",
  "printWidth": 100,
  "bracketSpacing": true,
  "arrowParens": "avoid"
}
```

## EditorConfig

```ini
# .editorconfig
root = true

[*]
indent_style = space
indent_size = 2
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true

[*.md]
trim_trailing_whitespace = false

[Makefile]
indent_style = tab
```

## Prettier Ignore

```
# .prettierignore
dist/
build/
node_modules/
coverage/
*.min.js
*.min.css
pnpm-lock.yaml
package-lock.json
```
</configuration>

<commands>
## Package.json Scripts

```json
{
  "scripts": {
    "format": "prettier --write .",
    "format:check": "prettier --check .",
    "format:staged": "prettier --write $(git diff --staged --name-only)"
  }
}
```

## Common Commands

```bash
# Check if files are formatted (CI)
pnpm format:check

# Format all files (new projects only!)
pnpm format

# Format only staged files (legacy projects)
pnpm format:staged

# Format specific file
pnpm prettier --write src/index.ts
```
</commands>

<editor_integration>
## VS Code Settings

```json
// .vscode/settings.json
{
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  // For NEW projects: enable format on save
  // For LEGACY projects: comment this out
  // "editor.formatOnSave": true
}
```

**Important:** `formatOnSave` should be disabled for legacy projects to avoid accidental mass reformatting.
</editor_integration>

<workflow>
## Recommended Workflow

**New Project:**
1. Set up Prettier + EditorConfig from start
2. Enable format on save
3. Run `pnpm format` freely

**Legacy Project:**
1. Add Prettier config (don't run yet!)
2. Disable format on save
3. Format only files you modify
4. Consider: One-time formatting commit (coordinate with team)

**One-Time Formatting Commit:**
```bash
# Do this on a clean branch
git checkout -b chore/format-codebase
pnpm format
git add -A
git commit -m "chore: Format entire codebase with Prettier"
# Merge as single commit, inform team
```
</workflow>

<eslint_integration>
## ESLint + Prettier

To avoid conflicts between ESLint and Prettier:

```bash
pnpm add -D eslint-config-prettier
```

```javascript
// eslint.config.js
import prettier from 'eslint-config-prettier';

export default [
  // ... other configs
  prettier, // Must be last to override other configs
];
```

This disables ESLint rules that conflict with Prettier.
</eslint_integration>
