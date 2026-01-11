# Linting Rules

<rules>
1. **Official tools only** - Use ESLint official packages, avoid unknown community plugins (security risk).
2. **Fix before commit** - All lint errors must be resolved before committing.
3. **Disable with reason** - `eslint-disable` only with comment explaining why.
4. **No blanket disables** - Never disable rules for entire files without review.
5. **Run in CI** - Linting must be part of CI pipeline.
</rules>

For details see `GUIDES/linting.md`
