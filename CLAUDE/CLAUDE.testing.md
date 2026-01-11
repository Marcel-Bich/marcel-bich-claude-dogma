# Testing Rules

<rules>
1. **Test pyramid** - Many unit tests, some integration, few E2E.
2. **Unit tests always run** - Run all unit tests before every commit.
3. **E2E tests filtered** - NEVER run all E2E tests. Use `--grep` to filter.
4. **Tests before commit** - No commit without passing tests.
5. **Coverage for critical code** - Aim for 80%+ on business logic.
</rules>

For details see `GUIDES/testing.md`
