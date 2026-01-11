# AI Traces Guide

<typography>
## Typography - Avoiding AI-Typical Characters

Certain characters reveal AI-generated content. Always use plain ASCII equivalents.

| Avoid | Unicode | Use Instead | Unicode |
|-------|---------|-------------|---------|
| " " | U+201C, U+201D (curly quotes) | " | U+0022 (straight quote) |
| ' ' | U+2018, U+2019 (smart apostrophes) | ' | U+0027 (straight apostrophe) |
| ‚ | U+201A (low-9 quote) | ' | U+0027 |
| -- | U+2014 (em-dash) | - or -- | U+002D |
| -- | U+2013 (en-dash) | - | U+002D |
| ... | U+2026 (ellipsis) | ... | Three dots |

**Why these matter:**
- AI models often produce these Unicode characters
- Human typing typically produces ASCII equivalents
- Presence of these characters can indicate AI-generated content
</typography>

<phrases>
## AI-Typical Phrases

Avoid these patterns in comments and documentation:

| Avoid | Why |
|-------|-----|
| "Let me..." | AI assistant pattern |
| "I'll..." | AI assistant pattern |
| "Sure!" | Overly eager response |
| "Certainly!" | Formal AI response |
| "Great question!" | Unnecessary validation |
| "I'd be happy to..." | AI politeness pattern |

**Better alternatives:**
- Just do the thing without announcing it
- Use direct, factual language
- Skip pleasantries in code comments
</phrases>

<emojis>
## Emojis in Code

**Never use emojis in:**
- Source code
- Comments
- Variable/function names
- Log messages
- Error messages

**Allowed in:**
- UI strings (user-facing output)
- Documentation (sparingly)
- Commit messages (if project convention)

**Rationale:** Emojis in code are unprofessional and often indicate AI generation.
</emojis>

<detection>
## Detection

The dogma `post-write-validate` hook automatically checks for these patterns after Write/Edit operations and warns if found.

**Manual check with grep:**
```bash
# Curly quotes (U+201C, U+201D)
grep -P '[\x{201C}\x{201D}]' file

# Smart apostrophes (U+2018, U+2019, U+201A)
grep -P '[\x{2018}\x{2019}\x{201A}]' file

# Em-dash and en-dash (U+2014, U+2013)
grep -P '[\x{2014}\x{2013}]' file

# Ellipsis (U+2026)
grep -P '[\x{2026}]' file
```

**Cleanup command:**
```bash
/dogma:cleanup
```
</detection>
