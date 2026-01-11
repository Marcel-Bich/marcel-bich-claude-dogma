# Testing Guide

<test_pyramid>
## Test Pyramid

```
        /\
       /  \      E2E Tests (few, slow, expensive)
      /----\
     /      \    Integration Tests (some, medium)
    /--------\
   /          \  Unit Tests (many, fast, cheap)
  /__________\
```

| Type | Quantity | Speed | Cost | Scope |
|------|----------|-------|------|-------|
| **Unit** | Many (70%) | Fast (ms) | Low | Single function/component |
| **Integration** | Some (20%) | Medium (s) | Medium | Multiple components |
| **E2E** | Few (10%) | Slow (min) | High | Full user flow |
</test_pyramid>

<unit_tests>
## Unit Tests (Vitest)

**Always run all unit tests** - they're fast enough.

```bash
pnpm test           # Run all unit tests
pnpm test:watch     # Watch mode during development
```

**Good unit test:**
```typescript
import { describe, it, expect } from 'vitest';
import { calculateTotal } from './cart';

describe('calculateTotal', () => {
  it('sums item prices', () => {
    const items = [{ price: 10 }, { price: 20 }];
    expect(calculateTotal(items)).toBe(30);
  });

  it('returns 0 for empty cart', () => {
    expect(calculateTotal([])).toBe(0);
  });

  it('applies discount correctly', () => {
    const items = [{ price: 100 }];
    expect(calculateTotal(items, 0.1)).toBe(90);
  });
});
```
</unit_tests>

<integration_tests>
## Integration Tests

**Run with real dependencies** (database, server, etc.)

```bash
pnpm test:integration    # Starts server automatically
```

**Characteristics:**
- Test component interactions
- May require setup/teardown
- Slower than unit tests
- Skip if server not available
</integration_tests>

<e2e_tests>
## E2E Tests (Playwright)

**CRITICAL: E2E tests are SLOW (5+ minutes for full suite)**

**NEVER run all E2E tests:**
```bash
# BAD - takes forever
pnpm test:e2e

# GOOD - filter by name
pnpm test:e2e --grep "login"
pnpm test:e2e --grep "checkout"
pnpm test:e2e --grep "navigation"
```

**Test chains:** Some tests depend on others (e.g., login before checkout). Run entire chain:
```bash
pnpm test:e2e --grep "auth|checkout"
```

**Debugging:**
```bash
pnpm test:e2e:slow     # Slow-mo for watching
pnpm test:e2e --debug  # Pause on failures
```
</e2e_tests>

<coverage>
## Coverage Targets

| Code Type | Target | Rationale |
|-----------|--------|-----------|
| Business logic | 80%+ | Critical paths must be tested |
| Utilities | 90%+ | Easy to test, high reuse |
| UI components | 60%+ | Harder to test, snapshot helps |
| Generated code | Skip | Don't test generated files |

```bash
pnpm test:coverage     # Generate coverage report
```

**Don't chase 100%** - diminishing returns after 80%.
</coverage>

<workflow>
## Testing Workflow

**During development:**
```bash
pnpm test:watch   # Tests run on file change
```

**Before commit:**
```bash
pnpm check        # lint + format:check + test
```

**Before merge:**
```bash
pnpm check
pnpm test:e2e --grep "relevant-feature"
```

**In CI:**
```yaml
- run: pnpm test
- run: pnpm test:e2e  # Full suite OK in CI
```
</workflow>

<commands>
## Quick Reference

```bash
# Unit tests
pnpm test              # Run all once
pnpm test:watch        # Watch mode
pnpm test:coverage     # With coverage

# Integration tests
pnpm test:integration  # With server

# E2E tests
pnpm test:e2e --grep "feature"  # ALWAYS filter!
pnpm test:e2e:slow              # Slow-mo for debugging

# All checks
pnpm check             # lint + format + test
pnpm check:all         # + integration + E2E
```
</commands>
