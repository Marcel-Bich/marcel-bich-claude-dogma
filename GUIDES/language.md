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
| Commit message (German) | Umlauts | `Groessenberechnung korrigiert` -> `Größenberechnung korrigiert` |
| PR title/body (German) | Umlauts | `Behebt fehlerhafte Groessenpruefung` -> `Behebt fehlerhafte Größenprüfung` |
| Variable names | ASCII | `const groesse = 10;` |
| Function names | ASCII | `function ueberpruefen()` |
| Filenames | ASCII | `groessen-helper.ts` |
| Class names | ASCII | `class GrafikBearbeiter` |
| Database columns | ASCII | `user_groesse` |
| API endpoints | ASCII | `/api/uebersicht` |
| Git branches | ASCII | `feature/groessen-anpassung` |

**Note:** This table only governs the umlaut-vs-ASCII split for text that IS German. Whether a given spot is German at all follows Language Selection below (established language wins, English as fallback).
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

Which natural language to write prose, comments and docs in. This is separate from the umlaut / ASCII rules above (those decide HOW to spell a given German text, not WHICH language to use).

**Precedence (highest first):**
1. **Explicit user request** - if the user asked for a specific language, use it.
2. **Tool / plugin language setting** - if a tool or plugin defines the language for its own content (e.g. a task/item system such as credo configured to a given language, or where items have so far been written in that language), that takes precedence over the defaults below. Keep using the language already established there.
3. **Established language at the spot** - use the language already in use where you are writing (adjacent comments, strings, docs, surrounding code). Consistency at that spot always wins; never translate existing content and never mix languages within a file.
4. **Default: English** - only for genuinely new content where no language is established. When in doubt, prefer English.

**When the correct language is genuinely unclear, ask the user instead of guessing.**

- **Exception - autonomous mode** (e.g. credo autonomous mode, or any other unattended/autonomous run): do NOT stop to ask. Proceed with the best choice and state a one-line reason for the language picked. The user can intervene or stop the run to correct what was written. Rationale: an autonomous run must not be blocked by such a minor question.

**User-facing UI / GUI strings and messages:** the UI language is a project decision - established by the strings already present OR by an explicit project convention/config. Follow that established UI language (it may well be German). Do NOT introduce new German (or any new language) just because a string is user-facing or the audience is assumed to speak it. Where nothing is established, default to English and confirm the intended UI language rather than guessing. Once German is the established UI language, the umlaut rules above apply to those strings.

**README and public documentation:** always English, for international readability - even in an otherwise non-English project.
</language_detection>
