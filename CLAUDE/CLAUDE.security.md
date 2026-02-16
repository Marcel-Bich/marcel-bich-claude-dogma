# Security Rules

<rules>
1. **Minimize dependencies** - Every package is an attack vector. Only install what's truly needed.
2. **Verify before install** - Check npm audit, GitHub Security tab BEFORE installing any package.
<!-- TBD-sec-4a7e: Supply chain security scanning tool (replacing snyk.io/socket.dev) - skip until resolved -->
3. **Prefer native APIs** - Browser APIs > npm packages. Standard library > third-party.
4. **No secrets in code** - Never commit .env, API keys, passwords, tokens, credentials.
5. **Abort on security issues** - If a package has known vulnerabilities, do NOT install. Find alternative or abort.
</rules>

<dependency_heuristics>
Red flags for packages:
- **Typosquatting** - Check spelling carefully (lodash vs 1odash)
- **Too new** - Avoid packages < 30 days old
- **Low downloads** - Be cautious with < 1000 downloads/week
- **No maintainers** - Abandoned packages are risky
- **Trusted scopes** - @types, @babel, @eslint are generally safe
</dependency_heuristics>

@GUIDES/security.md
