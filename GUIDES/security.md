# Security Guide

<supply_chain_attacks>
**Background:** Massive supply-chain attacks on npm packages in recent years. Every dependency is a potential attack vector.

**Hierarchy of trust:**
1. Native Browser/Runtime APIs (highest trust)
2. Standard library functions
3. Large established packages (React, Vue, Express)
4. Small packages with few dependencies
5. New/unknown packages (lowest trust - verify thoroughly)
</supply_chain_attacks>

<before_installing>
**ALWAYS check before installing ANY package:**

| Source | URL | What to check |
|--------|-----|---------------|
| Socket.dev | https://socket.dev/ | Supply chain risk score |
| Snyk Advisor | https://snyk.io/advisor/ | Package health, vulnerabilities |
| npm audit | `npm audit` / `pnpm audit` | Known vulnerabilities |
| GitHub | Security tab | Security advisories |

**Red flags - do NOT install:**
- Package with known vulnerabilities (unpatched)
- Very new package with no history
- Package with many dependencies
- Typosquatting (e.g., `lodash` vs `1odash`)
- Maintainer recently changed
- Suspicious install scripts
</before_installing>

<dependency_rules>
| Rule | Rationale |
|------|-----------|
| Fewer packages = less risk | Attack surface grows with each dependency |
| Prefer packages with few deps | Transitive dependencies are hidden risks |
| Large established > small unknown | More eyes on code, faster patches |
| Check last update date | Abandoned packages don't get security fixes |
| Pin versions in production | Avoid supply chain attacks via auto-updates |
</dependency_rules>

<secrets_management>
**Never commit:**
- `.env` files (use `.env.example` with placeholders)
- API keys, tokens, passwords
- Private keys, certificates
- Database connection strings with credentials
- OAuth secrets

**How to handle secrets:**
1. Use environment variables
2. Create `.env.example` with placeholder values
3. Add `.env*` to `.gitignore` (except `.env.example`)
4. Use secret managers in production (Vault, AWS Secrets Manager, etc.)

**If you accidentally commit a secret:**
1. Rotate the secret IMMEDIATELY
2. Use `git filter-branch` or BFG to remove from history
3. Force push (coordinate with team)
4. Consider the secret compromised regardless
</secrets_management>

<security_checklist>
Before any dependency change:

- [ ] Is this package really necessary?
- [ ] Can native APIs solve this instead?
- [ ] Checked socket.dev for supply chain risks?
- [ ] Checked snyk.io for vulnerabilities?
- [ ] Package actively maintained?
- [ ] Dependencies count acceptable?
- [ ] No suspicious install scripts?
</security_checklist>

<abort_conditions>
**STOP and inform user if:**
- Package has unpatched critical vulnerabilities
- Package flagged by socket.dev as high risk
- Package appears to be typosquatting
- No secure alternative exists for required functionality
- Installing would require disabling security features

**Never:**
- Ignore security warnings to "just make it work"
- Install packages without verification
- Commit secrets "temporarily"
</abort_conditions>
