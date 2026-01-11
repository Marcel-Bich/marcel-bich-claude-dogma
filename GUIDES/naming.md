# Naming Guide

<core_principle>
**Identical in DE+EN** - Names must work equally well in German and English contexts. Not similar, not translatable - identical.
</core_principle>

<naming_rules>
| Rule | Rationale |
|------|-----------|
| Confirm name before implementation | Renaming later is costly and error-prone |
| Clarity over brevity | `user-authentication-service` > `uas` |
| Consistent case per context | kebab-case for repos/folders, camelCase for code |
| No special characters | ASCII only (a-z, 0-9, hyphen, underscore) |
</naming_rules>

<prefixes>
| Prefix | Use for |
|--------|---------|
| `claude-` | Claude Code plugins, extensions, tools |
| `mcp-` | MCP servers |
| `lib-` | Shared libraries |
| `api-` | API services |
</prefixes>

<case_conventions>
| Context | Convention | Example |
|---------|------------|---------|
| Repository names | kebab-case | `my-project-name` |
| Folder names | kebab-case | `user-management/` |
| Package names | depends on ecosystem | npm: kebab, Python: snake_case |
| File names | kebab-case or snake_case | `user-service.ts`, `user_model.py` |
| Classes | PascalCase | `UserService` |
| Functions/methods | camelCase or snake_case | `getUserById`, `get_user_by_id` |
| Constants | SCREAMING_SNAKE | `MAX_RETRY_COUNT` |
</case_conventions>

<checklist>
Before finalizing a name:

1. [ ] Works identically in German and English?
2. [ ] Clear meaning without context?
3. [ ] No abbreviations that need explanation?
4. [ ] Follows ecosystem conventions?
5. [ ] Not already taken (check npm, PyPI, GitHub)?
</checklist>

<examples>
**Good names (identical DE+EN):**
- `petrischale` - Scientific term, same in both languages
- `schnellequalle` - Made-up word, no translation needed
- `dogma` - Same in both languages

**Bad names (translation needed):**
- `schnellstart` → DE: Schnellstart, EN: Quickstart
- `benutzer-service` → DE: Benutzer, EN: User
</examples>
