# Error Handling Rules

<rules>
1. **Never swallow errors** - Empty catch blocks are forbidden.
2. **Log with context** - Include relevant data, not just error message.
3. **User-friendly messages** - Technical errors become human-readable for users.
4. **Fail fast** - Validate early, crash on unrecoverable errors.
5. **Try/catch external calls** - Always wrap API, DB, file operations.
</rules>

For details see `GUIDES/error-handling.md`
