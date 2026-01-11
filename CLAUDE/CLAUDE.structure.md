# Structure Rules for Dogma Repo

<rules>
1. **CLAUDE/*.md** - Short rules (~10 lines), must be self-sufficient for normal use
2. **GUIDES/*.md** - Detailed conventions, only read when agent needs more context
3. **@ references** - For critical files that MUST always be loaded (CLAUDE or GUIDES)
4. **Backtick references** - For situational files, read only when relevant
5. **Situational loading** - Agent decides when to read based on task at hand
6. **Reference position** - Rules first, then reference to GUIDES at the end
</rules>

<reference_patterns>
```
@CLAUDE/file.md                  <- Critical: always loaded with parent
@GUIDES/file.md                  <- Critical: always loaded with parent (for critical dogmas)
`CLAUDE/file.md`                 <- Situational: agent reads when relevant
For details see `GUIDES/file.md` <- Optional: read if more context needed
```
</reference_patterns>

<file_purposes>
| Location | Purpose | When loaded |
|----------|---------|-------------|
| `CLAUDE.md` | Main entry point | Always |
| `CLAUDE/*.md` | Concise rules | Critical: with @, Others: when relevant |
| `GUIDES/*.md` | Detailed conventions | When agent needs context |
</file_purposes>

For details see `GUIDES/structure.md`
