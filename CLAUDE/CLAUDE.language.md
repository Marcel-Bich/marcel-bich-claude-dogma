# Language Rules

<rules>
**Language selection** (which natural language for prose/comments/docs) - precedence, highest first:
1. **Explicit user request** - a requested language wins.
2. **Tool/plugin setting** - a tool that sets its own content language (e.g. credo items) overrides the default.
3. **Existing language** - continue a file's language; never mix languages in one file.
4. **Default English** - new/unclear -> English. When genuinely unclear, ASK the user first. Exception: autonomous mode (e.g. credo autonomous, or any unattended run) -> do NOT ask, proceed and give a one-line reason; the user stops/corrects the run if needed.

**Always:**
- **README + public docs -> English** (international), even in a German project.
- **UI/GUI strings -> product locale/audience** (German app -> German strings), independent of code language.
- **German umlauts** - ALWAYS use ä, ö, ü, ß in German text. NEVER ae, oe, ue, ss.
- **ASCII identifiers** - For German text: use ae, oe, ue, ss in filenames, variables, functions (not umlauts).
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
