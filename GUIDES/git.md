# Git Conventions

<permissions>
## Git Permissions

The checkboxes in `CLAUDE.git.md` control autonomous git operations:

| Checkbox | Meaning |
|----------|---------|
| `- [ ]` | Not allowed - requires explicit user request |
| `- [x]` | Allowed - Claude may execute autonomously |

**Default behavior (all unchecked):**
- Claude does NOT perform git operations autonomously
- Every operation requires explicit user instruction
- "Please commit" or "push it" count as explicit instructions

**When enabled:**
- Claude can commit autonomously after completing tasks
- Useful for automated workflows with `--dangerously-skip-permissions`

**Recommendation:** Keep disabled by default. Only enable when consciously desired.
</permissions>

<file_protection>
## File Deletion Protection

Claude must NEVER delete local files without explicit user confirmation.

**Safe operations (no confirmation needed):**
| Command | Effect |
|---------|--------|
| `git rm --cached file` | Untracks file, keeps local copy |
| `git reset file` | Unstages file, keeps local copy |
| `git restore --staged file` | Unstages file, keeps local copy |

**Dangerous operations (ALWAYS ask first):**
| Command | Risk |
|---------|------|
| `rm`, `del`, `unlink` | Permanently deletes local file |
| `git clean` | Deletes ALL untracked files |
| `rmdir`, `rd` | Deletes directories |

**When user requests deletion:**
1. Explain what will be deleted
2. Ask for explicit confirmation, OR
3. Tell user how to do it themselves: `rm filename`

**Rationale:** Deleted files may be unrecoverable. User must consciously decide.
</file_protection>

<author_attribution>
AI-generated code should not receive author attribution in commits.

**Patterns to avoid:**
- `Co-Authored-By: <AI name> <...>`
- `Generated with [AI Tool](...)`
- Similar attribution texts

**Rationale:** The human developer is responsible for all committed code.
</author_attribution>

<commit_messages>
**Format for version bumps:**
```
vX.Y.Z: <description>
```

**General commit messages:**
- Be concise but descriptive
- Explain WHAT changed, not HOW (the diff shows how)
- Use imperative mood ("Add feature" not "Added feature")
</commit_messages>

<code_style>
Avoid emojis and unusual characters in:
- Code lines
- Comments
- Variable names

**Allowed in:**
- UI/GUI elements
- User-facing output
- Documentation (sparingly)

**Rationale:** Consistency, readability, encoding compatibility.
</code_style>

<agent_files>
In most repositories, these files are local-only and not versioned:

- `CLAUDE.md`
- `CLAUDE.*.md`
- `whats-next.md`
- Other agent/assistant configuration files

**Rationale:** Local configurations may vary per developer.

**Exception:** Repositories explicitly designed to version these files.
</agent_files>
