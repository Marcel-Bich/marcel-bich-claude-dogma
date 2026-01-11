# Linting Guide

<tool_selection>
## Recommended Linting Stack

| Language | Tool | Official Package |
|----------|------|------------------|
| JavaScript | ESLint | `eslint`, `@eslint/js` |
| TypeScript | ESLint + TS | `typescript-eslint` |
| Vue | ESLint + Vue | `eslint-plugin-vue` (official) |
| React | ESLint + React | `eslint-plugin-react` (official) |
| Svelte | ESLint + Svelte | `eslint-plugin-svelte` |

**Security-focused plugins (vetted):**
- `eslint-plugin-security` - Security-related rules
- `eslint-plugin-no-secrets` - Detect hardcoded secrets

**Avoid:**
- Unknown community plugins without security review
- Plugins with many dependencies
- Plugins not actively maintained
</tool_selection>

<eslint_config>
## ESLint Configuration (Flat Config - ESLint 9+)

```javascript
// eslint.config.js
import js from '@eslint/js';
import tseslint from 'typescript-eslint';

export default [
  js.configs.recommended,
  ...tseslint.configs.recommended,
  {
    rules: {
      // Customize rules here
      'no-console': 'warn',
      'no-unused-vars': 'error',
      '@typescript-eslint/no-explicit-any': 'warn',
    },
  },
  {
    ignores: ['dist/', 'node_modules/', 'coverage/'],
  },
];
```

## Package.json Scripts

```json
{
  "scripts": {
    "lint": "eslint .",
    "lint:fix": "eslint . --fix"
  }
}
```
</eslint_config>

<disabling_rules>
## When to Disable Rules

**Acceptable:**
```javascript
// eslint-disable-next-line no-console -- Debug output for development only
console.log('Debug:', data);

/* eslint-disable @typescript-eslint/no-explicit-any --
   Third-party library has incorrect types,
   TODO: Remove when types are fixed in v2.0 */
```

**Not acceptable:**
```javascript
// eslint-disable-next-line -- just disable it
// (No explanation = not acceptable)

/* eslint-disable */
// (Blanket disable for entire file = not acceptable)
```

**Rules for disabling:**
1. Always explain WHY the rule is disabled
2. Use most specific disable (single line > block > file)
3. Add TODO if it's temporary
4. Review disabled rules periodically
</disabling_rules>

<commands>
## Common Commands

```bash
# Check for issues
pnpm lint

# Auto-fix what's possible
pnpm lint:fix

# Check specific files
pnpm lint src/components/

# Show only errors (no warnings)
pnpm lint --quiet
```
</commands>

<ci_integration>
## CI Pipeline Integration

```yaml
# .github/workflows/lint.yml
name: Lint
on: [push, pull_request]
jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: pnpm/action-setup@v2
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'pnpm'
      - run: pnpm install
      - run: pnpm lint
```

**CI must fail on lint errors** - never merge code with lint errors.
</ci_integration>

<editor_integration>
## Editor Setup

**VS Code:**
```json
// .vscode/settings.json
{
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": "explicit"
  },
  "eslint.validate": ["javascript", "typescript", "vue"]
}
```

**Note:** Auto-fix on save is optional and should respect the project's formatting toggle setting (see formatting.md).
</editor_integration>
