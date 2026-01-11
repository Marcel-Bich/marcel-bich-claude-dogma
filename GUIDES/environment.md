# Environment Guide

<file_hierarchy>
| File | Purpose | Committed? |
|------|---------|------------|
| `.env.example` | Template with placeholders | Yes |
| `.env` | Local defaults (shared) | No |
| `.env.local` | Personal overrides | No |
| `.env.production` | Production values | No |
| `.env.test` | Test environment | No |

**Loading order (later overrides earlier):**
1. Defaults in code
2. `.env`
3. `.env.local`
4. `.env.[mode]` (development, production, test)
5. `.env.[mode].local`
6. Actual environment variables (runtime)
</file_hierarchy>

<env_example_format>
```bash
# .env.example - Template for environment variables
# Copy to .env and fill in values

# =============================================================================
# Application
# =============================================================================
NODE_ENV=development
PORT=3000

# =============================================================================
# Database
# =============================================================================
DATABASE_URL=postgresql://user:password@localhost:5432/dbname

# =============================================================================
# Authentication
# =============================================================================
JWT_SECRET=your-secret-key-here
SESSION_SECRET=another-secret-key

# =============================================================================
# External Services
# =============================================================================
# Get your API key at https://example.com/api-keys
API_KEY=your-api-key-here
```

**Rules for .env.example:**
- Use descriptive placeholder values
- Group related variables with headers
- Add comments explaining where to get values
- Never include real secrets, even "test" ones
</env_example_format>

<naming_conventions>
| Pattern | Use for | Example |
|---------|---------|---------|
| `SCREAMING_SNAKE` | All env vars | `DATABASE_URL` |
| `_URL` suffix | Connection strings | `REDIS_URL` |
| `_KEY` suffix | API keys | `STRIPE_KEY` |
| `_SECRET` suffix | Secrets | `JWT_SECRET` |
| `_HOST`, `_PORT` | Network config | `DB_HOST`, `DB_PORT` |
| `ENABLE_`, `DISABLE_` | Feature flags | `ENABLE_DEBUG` |
</naming_conventions>

<defaults_in_code>
```typescript
// Good: Default in code, overridable via env
const port = process.env.PORT ?? 3000;
const debug = process.env.DEBUG === 'true';

// Good: Fail fast if required var missing
const apiKey = process.env.API_KEY;
if (!apiKey) {
  throw new Error('API_KEY environment variable is required');
}

// Bad: Hardcoded value
const port = 3000;  // Can't be changed without code change

// Bad: Secret in code
const apiKey = 'sk_live_abc123';  // NEVER do this
```
</defaults_in_code>

<validation>
**Validate environment at startup:**

```typescript
// config.ts
const requiredEnvVars = [
  'DATABASE_URL',
  'JWT_SECRET',
  'API_KEY',
] as const;

for (const envVar of requiredEnvVars) {
  if (!process.env[envVar]) {
    throw new Error(`Missing required environment variable: ${envVar}`);
  }
}

export const config = {
  database: {
    url: process.env.DATABASE_URL!,
  },
  jwt: {
    secret: process.env.JWT_SECRET!,
    expiresIn: process.env.JWT_EXPIRES_IN ?? '7d',
  },
  // ...
} as const;
```

**Benefits:**
- Fails fast at startup, not at runtime
- Single source of truth for config
- Type-safe access throughout app
</validation>

<gitignore_pattern>
```gitignore
# Environment files
**/.env
**/.env.*
!**/.env.example
```

This ignores all .env files EXCEPT .env.example.
</gitignore_pattern>
