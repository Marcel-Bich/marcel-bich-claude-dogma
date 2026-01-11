# Philosophy Guide

Core development principles that underpin all other guidelines.

<yagni>
## YAGNI - You Aren't Gonna Need It

**Principle:** Only implement what's needed RIGHT NOW.

**Don't:**
- Add features "for later"
- Build "flexible" architecture without concrete need
- Create abstractions for hypothetical use cases
- Add config options nobody asked for

**Do:**
- Solve today's problem today
- Add complexity only when requirement exists
- Delete unused code immediately

**Security benefit:** Less code = smaller attack surface, fewer dependencies = less risk.

```typescript
// BAD: "Might need this later"
class UserService {
  private cache: Map<string, User>;
  private retryPolicy: RetryPolicy;
  private circuitBreaker: CircuitBreaker;
  // ... 500 lines for 2 actual use cases
}

// GOOD: What we actually need
async function getUser(id: string): Promise<User> {
  return await db.users.findById(id);
}
```
</yagni>

<kiss>
## KISS - Keep It Simple, Stupid

**Principle:** Choose the simplest solution that works.

**Readability > Performance** (unless you've MEASURED a bottleneck)

```typescript
// KISS - Clear and obvious
const names = users.map(u => u.name);

// Not KISS - Unnecessarily complex
const names = users.reduce((acc, u) => [...acc, u.name], []);

// KISS - Simple conditional
if (user.isAdmin) {
  showAdminPanel();
}

// Not KISS - Over-engineered
const strategies = {
  admin: () => showAdminPanel(),
  user: () => null,
};
strategies[user.role]?.();
```

**Test:** Can a junior developer understand this in 30 seconds?
</kiss>

<rule_of_three>
## Rule of Three (WET before DRY)

**Principle:** Don't abstract until the 3rd repetition.

| Acronym | Meaning | When |
|---------|---------|------|
| DRY | Don't Repeat Yourself | After 3rd repetition |
| WET | Write Everything Twice | Acceptable duplication |
| WETTER | Write Everything Three Times, then Extract | Optimal approach |

**Why wait?**
- 1st time: You don't know the pattern yet
- 2nd time: You see similarity but not the right abstraction
- 3rd time: NOW you understand what to extract

**Premature abstraction is worse than duplication:**
- Wrong abstraction is hard to fix
- Duplication is easy to refactor later
- Copy-paste is honest; bad abstraction hides complexity

```typescript
// After 3rd similar function, THEN extract:
function formatDate(date: Date, locale: string): string {
  // Now we know what parameters we actually need
}
```
</rule_of_three>

<small_functions>
## Small Functions

**Metrics:**
| Metric | Limit | Why |
|--------|-------|-----|
| Lines | 20-30 max | Fits on one screen |
| Parameters | 3-4 max | Easy to understand |
| Nesting | 2-3 levels | Reduces complexity |
| Cyclomatic Complexity | < 10 | Testable |

**One function = One task**

```typescript
// BAD: Does too much
function processUser(data: unknown) {
  // validate (10 lines)
  // transform (15 lines)
  // save (10 lines)
  // notify (10 lines)
  // log (5 lines)
}

// GOOD: Single responsibility
function validateUser(data: unknown): UserInput { ... }
function transformUser(input: UserInput): User { ... }
function saveUser(user: User): Promise<void> { ... }
function notifyUserCreated(user: User): void { ... }
```

**Rule of thumb:** If you need to scroll, it's too long.
</small_functions>

<monolith_first>
## Start Monolith

**Principle:** Don't distribute until you must.

| Phase | Architecture | When to move on |
|-------|--------------|-----------------|
| MVP/Prototype | Monolith | Never (often enough) |
| Growth | Modular Monolith | Team coordination issues |
| Scale | Microservices | Independent deployment needed |

**Monolith advantages:**
- Simple deployment (one artifact)
- Easy debugging (one process)
- No network latency between components
- Refactoring is straightforward

**Microservices only when:**
- Different parts need different scaling
- Teams can't work in same codebase
- Independent deployment is required
- You have DevOps capacity to manage it

```
project/
├── src/
│   ├── users/      # Module, not service
│   ├── orders/     # Module, not service
│   └── shared/     # Shared utilities
└── package.json    # One deployable
```
</monolith_first>

<composition>
## Composition over Inheritance

**Principle:** Prefer composition. Use inheritance only for true "is-a" relationships.

**Max inheritance depth:** 2 levels

```typescript
// BAD: Deep inheritance
class Animal { }
class Mammal extends Animal { }
class Dog extends Mammal { }
class GermanShepherd extends Dog { }  // Too deep!

// GOOD: Composition
interface CanBark { bark(): void; }
interface CanFetch { fetch(): void; }

class Dog implements CanBark, CanFetch {
  private barker = new Barker();
  private fetcher = new Fetcher();

  bark() { this.barker.bark(); }
  fetch() { this.fetcher.fetch(); }
}
```

**When inheritance IS appropriate:**
- True "is-a" relationship (Square is-a Rectangle: debatable!)
- Framework requires it (React class components, legacy)
- Shared implementation, not just interface
</composition>

<readability>
## Readability > Cleverness

**Code is read 10x more than written.**

```typescript
// Clever but hard to read
const r = d.reduce((a,c) => ({...a,[c.k]:c.v}),{});

// Readable
const result: Record<string, Value> = {};
for (const item of data) {
  result[item.key] = item.value;
}
```

**Naming matters more than comments:**
```typescript
// BAD: Comment explains bad name
const d = 86400; // seconds in a day

// GOOD: Name is self-documenting
const SECONDS_PER_DAY = 86400;
```

**If you need a comment to explain WHAT, rename instead.**
**Comments should explain WHY, not WHAT.**
</readability>

<summary>
## Quick Reference

| Principle | One-liner |
|-----------|-----------|
| YAGNI | Build for today, not tomorrow |
| KISS | Simplest solution wins |
| Rule of Three | Abstract on 3rd repetition |
| Small Functions | 20-30 lines, one task |
| Monolith First | Distribute only when forced |
| Composition | Combine behaviors, don't inherit |
| Readability | Clear > Clever |
</summary>
