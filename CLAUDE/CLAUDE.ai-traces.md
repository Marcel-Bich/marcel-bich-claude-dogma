# AI Traces Rules

<rules>
1. **No curly quotes** - Use straight quotes " (U+0022), never curly quotes (U+201C/U+201D) or smart apostrophes (U+2018/U+2019)
2. **No double-dashes** - Never em-dash (U+2014) or en-dash (U+2013); use - (U+002D). "--" is ONLY allowed where changing it to "-" would break functionality (CLI flags like --force, argument separators like git checkout -- file); in prose, docs, comments (including code comments) and strings always use "-".
3. **No smart ellipsis** - Use three dots (...), never the ellipsis character (U+2026)
4. **No AI phrases** - Avoid "Let me...", "I'll...", "Sure!", "Certainly!", "Great question!", "I'd be happy to..."
5. **No emojis in code** - Not in source, comments, identifiers, or logs. Only in UI/user output.
</rules>

For details see `GUIDES/ai-traces.md`
