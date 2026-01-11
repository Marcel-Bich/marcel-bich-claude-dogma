# Documentation Guide

<readme_structure>
## README Template

```markdown
# Project Name

Brief description of what this project does.

## Quick Start

\`\`\`bash
pnpm install
pnpm dev
\`\`\`

## Features

- Feature 1
- Feature 2

## Development

### Prerequisites

- Node.js 20+
- pnpm 8+

### Setup

\`\`\`bash
git clone <repo>
cd <project>
pnpm install
cp .env.example .env
pnpm dev
\`\`\`

### Commands

| Command | Description |
|---------|-------------|
| `pnpm dev` | Start development server |
| `pnpm build` | Build for production |
| `pnpm test` | Run tests |

## License

MIT
```
</readme_structure>

<comments>
## When to Comment

**Comment the WHY, not the WHAT:**

```typescript
// BAD: Explains what (obvious from code)
// Increment counter by 1
counter++;

// GOOD: Explains why (not obvious)
// Offset by 1 because array is 0-indexed but IDs start at 1
counter++;

// BAD: Obvious
// Check if user is logged in
if (user.isLoggedIn) { ... }

// GOOD: Non-obvious business rule
// Premium features require both login AND active subscription
if (user.isLoggedIn && user.subscription.isActive) { ... }
```

**When to comment:**
- Complex algorithms
- Non-obvious business rules
- Workarounds for bugs/limitations
- TODO items with context
- Regular expressions

**When NOT to comment:**
- Self-explanatory code
- What the code does (if readable)
- Obvious function purposes
</comments>

<jsdoc>
## JSDoc for Public APIs

```typescript
/**
 * Calculates the total price including discounts and tax.
 *
 * @param items - Cart items to calculate
 * @param discount - Discount percentage (0-1), e.g., 0.1 for 10%
 * @returns Total price after discount and tax
 *
 * @example
 * const total = calculateTotal(cartItems, 0.1);
 * console.log(`Total: $${total}`);
 */
export function calculateTotal(
  items: CartItem[],
  discount: number = 0
): number {
  // Implementation
}
```

**Document:**
- Exported functions
- Class methods
- Configuration options
- Complex types

**Skip documentation for:**
- Internal/private functions
- Self-explanatory getters/setters
- Trivial utilities
</jsdoc>

<changelog>
## CHANGELOG Format

Follow [Keep a Changelog](https://keepachangelog.com/):

```markdown
# Changelog

## [1.2.0] - 2024-01-15

### Added
- User authentication with OAuth

### Changed
- Improved loading performance

### Fixed
- Login timeout issue (#123)

### Removed
- Deprecated v1 API endpoints

## [1.1.0] - 2024-01-01
...
```

**Categories:**
- Added - New features
- Changed - Changes to existing functionality
- Deprecated - Features to be removed
- Removed - Removed features
- Fixed - Bug fixes
- Security - Security fixes
</changelog>

<inline_docs>
## Inline Documentation Patterns

```typescript
// TODO: Refactor when API v2 is released
// Currently using workaround for rate limiting bug

// FIXME: This breaks with > 1000 items
// See: https://github.com/org/repo/issues/123

// HACK: Safari requires this timeout
// Remove when Safari 17 drops support

// NOTE: Order matters here - auth must come before logging
middleware.use(auth);
middleware.use(logging);

// WARNING: Mutates the original array
// Use [...arr].sort() if original must be preserved
```

**Standard tags:**
- `TODO:` - Future improvement
- `FIXME:` - Known bug/issue
- `HACK:` - Workaround, not ideal
- `NOTE:` - Important information
- `WARNING:` - Potential pitfall
</inline_docs>
