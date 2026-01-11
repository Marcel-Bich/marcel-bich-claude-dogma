# Build Rules

<rules>
1. **Vite as default** - Use Vite for modern web projects (fast, simple, ESM-native).
2. **Vitest for tests** - Use Vitest (Vite-native) instead of Jest.
3. **Avoid complexity** - No Webpack unless absolutely required (legacy projects).
4. **TypeScript via Vite** - Let Vite handle TS transpilation, no separate tsc build.
5. **pnpm preferred** - Use pnpm over npm/yarn (faster, stricter, disk-efficient).
</rules>

For details see `GUIDES/build.md`
