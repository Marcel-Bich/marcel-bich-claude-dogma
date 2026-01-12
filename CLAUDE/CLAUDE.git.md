# Git Rules

@DOGMA-PERMISSIONS.md

<file_protection>
**NEVER delete local files without explicit user confirmation.**

Allowed without asking:
- `git rm --cached` (untrack but keep local file)
- `git reset` (unstage changes)
- Remove from .gitignore

NOT allowed without asking:
- `rm`, `del`, `unlink` on any file
- `git clean` (deletes untracked files)
- Any operation that removes local file content

When user wants file deleted: Explain how they can do it themselves.
</file_protection>

<rules>
1. **No AI attribution** - Never use Co-Authored-By with Claude/Anthropic/AI, no "Generated with Claude", no AI credits
2. **No emojis in code** - Not in source, comments, or identifiers. Only in UI/user output.
3. **Agent files** - Check if repo versions them before committing CLAUDE.* files
4. **Commit prefix** - Use `vX.Y.Z:` format for version bumps
</rules>

<ai_traces>
Avoid patterns that reveal AI usage:
- **Typography** - Use straight quotes " (U+0022), normal dashes - (U+002D), three dots (...) - never curly quotes " " (U+201C/U+201D), em-dashes -- (U+2014), smart apostrophes ' ' (U+2018/U+2019), or ellipsis ... (U+2026)
- **Phrases** - Avoid "Let me...", "I'll...", "Sure!", "Certainly!", "Great question!"
- **Emojis** - Never in code comments or logs
</ai_traces>

@GUIDES/git.md
@GUIDES/ai-traces.md
