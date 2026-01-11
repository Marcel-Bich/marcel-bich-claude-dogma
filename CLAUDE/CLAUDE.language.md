# Language Rules

<rules>
1. **Follow project conventions** - Match existing language in the project
2. **Maintain existing language** - Never translate or switch languages mid-file
3. **Default English** - When unsure or for new projects, use English as fallback
4. **German umlauts** - ALWAYS use ä, ö, ü, ß in German text. NEVER ae, oe, ue, ss.
5. **ASCII identifiers** - For German text: use ae, oe, ue, ss in filenames, variables, functions (not umlauts)
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
