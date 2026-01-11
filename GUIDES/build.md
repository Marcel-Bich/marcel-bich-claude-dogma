# Build Guide

<recommended_stack>
## Modern Web Stack

| Tool | Purpose | Why |
|------|---------|-----|
| **Vite** | Build/Dev server | Fast, simple, ESM-native, great DX |
| **Vitest** | Testing | Vite-native, Jest-compatible API |
| **pnpm** | Package manager | Fast, strict, disk-efficient |
| **ESBuild** | Bundling (via Vite) | Extremely fast |
| **TypeScript** | Type checking | Via Vite, no separate build step |

**This stack is used in:** schnellequalle, petrischale
</recommended_stack>

<vite_setup>
## Vite Configuration

```typescript
// vite.config.ts
import { defineConfig } from 'vite';

export default defineConfig({
  build: {
    target: 'esnext',
    sourcemap: true,
  },
  server: {
    port: 3000,
    host: true, // Allow LAN access
  },
});
```

## With Framework (Vue/React/Svelte)

```typescript
// vite.config.ts
import { defineConfig } from 'vite';
import vue from '@vitejs/plugin-vue';
// or: import react from '@vitejs/plugin-react';

export default defineConfig({
  plugins: [vue()],
});
```
</vite_setup>

<vitest_setup>
## Vitest Configuration

```typescript
// vitest.config.ts
import { defineConfig } from 'vitest/config';

export default defineConfig({
  test: {
    globals: true,
    environment: 'node', // or 'jsdom' for browser
    coverage: {
      reporter: ['text', 'html'],
    },
  },
});
```

Or extend vite.config.ts:

```typescript
// vite.config.ts
import { defineConfig } from 'vite';

export default defineConfig({
  // ... vite config
  test: {
    globals: true,
  },
});
```
</vitest_setup>

<package_scripts>
## Package.json Scripts

```json
{
  "scripts": {
    "dev": "vite",
    "dev:lan": "vite --host",
    "build": "vite build",
    "preview": "vite preview",
    "test": "vitest run",
    "test:watch": "vitest",
    "test:coverage": "vitest run --coverage",
    "lint": "eslint .",
    "lint:fix": "eslint . --fix",
    "format": "prettier --write .",
    "format:check": "prettier --check .",
    "check": "pnpm lint && pnpm format:check && pnpm test"
  }
}
```

**Note:** Use `dev:lan` for mobile testing (exposes to local network).
</package_scripts>

<typescript_handling>
## TypeScript with Vite

**Vite handles TypeScript automatically:**
- Transpiles TS to JS using ESBuild (very fast)
- Does NOT type-check during build (by design)

**For type checking:**
```json
{
  "scripts": {
    "typecheck": "tsc --noEmit",
    "check": "pnpm typecheck && pnpm lint && pnpm test"
  }
}
```

**tsconfig.json:**
```json
{
  "compilerOptions": {
    "target": "ESNext",
    "module": "ESNext",
    "moduleResolution": "bundler",
    "strict": true,
    "noEmit": true,
    "skipLibCheck": true
  },
  "include": ["src"]
}
```
</typescript_handling>

<avoid>
## What to Avoid

| Tool | Why avoid | When acceptable |
|------|-----------|-----------------|
| **Webpack** | Complex, slow, legacy | Legacy projects, specific requirements |
| **Create React App** | Deprecated, slow, inflexible | Never for new projects |
| **Parcel** | Less ecosystem support | Small projects with zero-config need |
| **npm/yarn** | Slower, less strict | Team already uses it |
| **Rollup directly** | More config needed | Library bundling (Vite uses it internally) |

**Exceptions:**
- Existing projects: Don't rewrite build system just for this
- Specific requirements: Some edge cases need Webpack plugins
</avoid>

<commands>
## Common Commands

```bash
# Development
pnpm dev          # Start dev server
pnpm dev:lan      # Start with LAN access (mobile testing)

# Building
pnpm build        # Production build
pnpm preview      # Preview production build locally

# Testing
pnpm test         # Run tests once
pnpm test:watch   # Run tests in watch mode
pnpm test:coverage # Run with coverage

# Quality
pnpm check        # Run all checks (lint + format + test)
```
</commands>
