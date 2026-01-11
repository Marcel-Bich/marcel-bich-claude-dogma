# Structure Guide for Dogma Repo

<reference_system>
<critical_references>
**@ syntax** - File is loaded automatically with its parent.

Use for:
- Rules that apply to EVERY task
- Content that would cause errors if missed
- Both CLAUDE/*.md and GUIDES/*.md can be @-referenced

Example in CLAUDE.md (critical CLAUDE file):
```
@CLAUDE/CLAUDE.git.md
```

Example in CLAUDE/*.md (critical GUIDES):
```
<rules>
1. ...
</rules>

@GUIDES/git.md
```

**Current critical chain:**
CLAUDE.md → @CLAUDE/CLAUDE.git.md → @GUIDES/git.md
</critical_references>

<situational_references>
**Backtick syntax** - Agent reads when task is relevant.

Use for:
- Rules that apply to specific tasks
- Content that adds context but isn't always needed
- Most GUIDES/* files

Example in CLAUDE.md:
```
<situational_rules>
- `CLAUDE/CLAUDE.versioning.md` - when bumping versions
</situational_rules>
```

Example in CLAUDE/*.md (optional GUIDES):
```
<rules>
1. ...
</rules>

For details see `GUIDES/versioning.md`
```
</situational_references>
</reference_system>

<content_guidelines>
<claude_files>
**CLAUDE/*.md - Rule files**

- Max ~10-15 lines
- Numbered rules, imperative mood
- Must be self-sufficient for 90% of cases
- Rules FIRST, then reference to GUIDES at the END

Structure (optional GUIDES):
```markdown
# [Topic] Rules

<rules>
1. **Rule name** - Brief explanation
2. **Rule name** - Brief explanation
</rules>

For details see `GUIDES/[topic].md`
```

Structure (critical GUIDES):
```markdown
# [Topic] Rules

<rules>
1. **Rule name** - Brief explanation
2. **Rule name** - Brief explanation
</rules>

@GUIDES/[topic].md
```
</claude_files>

<guides_files>
**GUIDES/*.md - Convention files**

- Detailed explanations with rationale
- Most important/critical info FIRST
- Examples and edge cases AFTER
- Tables for quick reference
- Workflow descriptions at the END
</guides_files>
</content_guidelines>

<directory_layout>
```
.
├── CLAUDE.md                 # Main entry point (always loaded)
├── CLAUDE/                   # Rule files (concise, actionable)
│   ├── CLAUDE.git.md         # Critical - loaded via @ in CLAUDE.md
│   ├── CLAUDE.versioning.md  # Situational - loaded when bumping versions
│   └── CLAUDE.structure.md   # Situational - loaded when modifying structure
├── GUIDES/                   # Convention files (detailed, explanatory)
│   ├── git.md
│   ├── versioning.md
│   └── structure.md
├── .gitignore                # Universal .gitignore
└── gitconfig                 # Git user configuration template
```
</directory_layout>

<token_efficiency>
**Goal:** Minimize tokens loaded per prompt while maintaining effectiveness.

**Hierarchy:**
1. CLAUDE.md (~50 lines) - Always loaded
2. @-referenced files - Always loaded with parent
3. Situational files - Only when task requires
4. GUIDES files - Only when agent needs more context

**Result:** Most prompts load ~100 lines instead of ~300+
</token_efficiency>
