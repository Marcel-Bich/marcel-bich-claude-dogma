# Language Guide

<umlaut_rules>
## German Umlauts and Eszett

**Note:** These rules apply only to German text. English words like "blue", "queue", "pass" are unaffected.

German text MUST use proper Unicode characters:

| Wrong | Right | Character |
|-------|-------|-----------|
| ae | ä | U+00E4 |
| oe | ö | U+00F6 |
| ue | ü | U+00FC |
| Ae | Ä | U+00C4 |
| Oe | Ö | U+00D6 |
| Ue | Ü | U+00DC |
| ss | ß | U+00DF |

**Note:** "ss" vs "ß" depends on spelling rules (e.g., "dass" not "daß" in new orthography).
</umlaut_rules>

<where_to_use>
## Where to Use What

| Context | Use | Example |
|---------|-----|---------|
| UI strings | Umlauts | `"Größe ändern"` |
| Error messages | Umlauts | `"Datei konnte nicht gefunden werden"` |
| Comments (German) | Umlauts | `// Überprüft die Größe` |
| Documentation | Umlauts | `## Übersicht` |
| Variable names | ASCII | `const groesse = 10;` |
| Function names | ASCII | `function ueberpruefen()` |
| Filenames | ASCII | `groessen-helper.ts` |
| Class names | ASCII | `class GrafikBearbeiter` |
| Database columns | ASCII | `user_groesse` |
| API endpoints | ASCII | `/api/uebersicht` |
| Git branches | ASCII | `feature/groessen-anpassung` |
</where_to_use>

<rationale>
## Why This Distinction?

**Umlauts in text:**
- Proper German orthography
- Better readability for German speakers
- Professional appearance

**ASCII in identifiers:**
- Cross-platform compatibility (some systems struggle with Unicode filenames)
- Easier to type on non-German keyboards
- Avoids encoding issues in URLs, APIs, databases
- Consistent with most coding conventions
</rationale>

<common_mistakes>
## Common Mistakes to Avoid

```typescript
// WRONG - ASCII in user-facing string
const message = "Datei wurde erfolgreich geloescht";

// RIGHT - Umlauts in user-facing string
const message = "Datei wurde erfolgreich gelöscht";

// WRONG - Umlauts in variable name (encoding issues)
const größe = 100;

// RIGHT - ASCII in variable name
const groesse = 100;

// WRONG - Mixed in same context
console.log("Größe: " + groesse + " für " + "fuer");

// RIGHT - Consistent
console.log("Größe: " + groesse + " für Benutzer");
```
</common_mistakes>

<language_detection>
## Language Selection

**Priority order:**
1. **Follow project conventions** - Match existing language in the project
2. **Maintain existing language** - Never translate or switch languages mid-file
3. **Default English** - When unsure or for new projects, use English as fallback

When editing a file:
1. Check existing comments and strings for language
2. Continue in that language
3. Never translate existing content
4. New additions match existing style
</language_detection>
