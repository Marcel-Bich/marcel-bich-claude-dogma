# Language Rules

<rules>
**Language selection** (which natural language for prose/comments/docs) - precedence, highest first:
1. **Explicit user request** - a requested language wins.
2. **Tool/plugin setting** - a tool that sets its own content language (e.g. credo items) overrides the default.
3. **Established language wins** - use the language already present where you write (adjacent comments, strings, docs, code); never translate existing content or mix languages in one file.
4. **Default English** - only for genuinely new content with no established language; when in doubt, English. When truly unclear, ASK first. Exception: autonomous mode (e.g. credo autonomous, or any unattended run) -> do NOT ask, proceed and give a one-line reason; the user stops/corrects the run if needed.

**Always:**
- **UI/GUI strings** - the UI language is a project decision (established strings or explicit convention). Follow it - it may be German. Do NOT introduce new German just because a string is user-facing or the audience seems German; nothing established -> English, confirm rather than guess.
- **README + public docs -> English** (international), even in a German project.
- **German umlauts** - ALWAYS use ä, ö, ü, ß in German text. NEVER ae, oe, ue, ss.
- **ASCII identifiers** - identifiers (variables, functions, filenames, classes, DB columns, API paths, branches) are ASCII regardless of the text language.
</rules>

<examples>
WRONG: "fuer", "koennen", "groesse", "aehnlich", "ueberpruefung"
RIGHT: "für", "können", "Größe", "ähnlich", "Überprüfung"

Exception (code identifiers):
- Variable: `const groesseInBytes = 100;` ← ASCII OK
- Filename: `ueberpruefung.ts` ← ASCII OK
- UI string: `"Überprüfung läuft..."` ← Umlauts required
</examples>

For details see `GUIDES/language.md`
