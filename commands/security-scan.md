# Command: security-scan

**Invokes:** `security-reviewer`
**Use when:** before deployment, or on demand for any
security-sensitive change.

## Instruction
Run `workflows/security-review.md` against the current diff or
design, using `security-checklist-owasp` and
`secure-configuration-secrets`.

## Output
A findings list with severity and concrete fixes, or an explicit
sign-off.
