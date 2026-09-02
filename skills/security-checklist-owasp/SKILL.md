---
skill: security-checklist-owasp
used_by: [security-reviewer, backend-engineer, frontend-engineer]
---

# Security Checklist (OWASP-aligned)

Run through this list for any change touching input handling,
authentication, or data exposure:

- **Injection**: are all SQL queries parameterized (no string
  concatenation of user input into T-SQL)?
- **Broken authentication**: are sessions/tokens issued and validated
  correctly, with sane expiry?
- **Broken access control**: is authorization checked per-resource,
  not just per-endpoint?
- **XSS**: is user-supplied content escaped/sanitized before
  rendering, especially in React `dangerouslySetInnerHTML` or
  any raw HTML injection point?
- **CSRF**: are state-changing requests protected (anti-forgery
  tokens or same-site cookies) where cookie-based auth is used?
- **Sensitive data exposure**: is personal/sensitive data encrypted at
  rest and in transit, and excluded from logs?
- **Security misconfiguration**: are default credentials, verbose
  error pages, and debug endpoints disabled in production?
- **Vulnerable dependencies**: are NuGet/npm packages checked against
  known CVEs before/while they're added?
- **Insufficient logging**: are auth failures and access-control
  denials logged (without logging secrets)?
