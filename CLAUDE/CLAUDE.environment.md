# Environment Rules

<rules>
1. **Never commit .env** - Only `.env.example` with placeholder values goes into git.
2. **Defaults in code** - Sensible defaults, overridable via environment variables.
3. **Hierarchy** - Defaults < .env < .env.local < Environment Variables (runtime wins).
4. **No hardcoded secrets** - All secrets via environment, never in source code.
5. **Document all variables** - Every env var must be in `.env.example` with description.
</rules>

For details see `GUIDES/environment.md`
