# Workflow: Security Review

**Agent(s):** `security-reviewer`
**Skills:** `security-checklist-owasp`, `secure-configuration-secrets`
**Stage input:** A design (from `architecture-design`) or a code diff.
**Stage output:** A findings list (severity, risk, concrete fix) or
an explicit sign-off.

## Steps
1. Run the relevant checklist items from `security-checklist-owasp`
   against the design/diff.
2. Check configuration/secret handling per
   `secure-configuration-secrets` if the change touches configuration,
   deployment, or credentials.
3. For each finding: state severity, the specific risk, and a concrete
   fix — not a vague instruction.
4. Route findings back to the originating engineer agent; re-review
   the fix before sign-off.

## Exit criteria
No open findings above an agreed severity threshold, or each remaining
finding has an explicit, documented risk-acceptance decision.

## Handoff
→ `code-review` (if not already done) → `deployment`.
