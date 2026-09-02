# Workflow: Testing

**Agent(s):** `qa-engineer`
**Skills:** `dotnet-testing`, `frontend-testing-and-accessibility`,
`mobile-testing`, `e2e-testing`
**Stage input:** Implemented code + the originating acceptance
criteria.
**Stage output:** A test plan/report and the tests themselves (or a
gap list).

## Steps
1. Map each acceptance criterion to at least one test.
2. Choose test layers appropriate to the change (unit for logic,
   integration/API for cross-boundary behavior, E2E only for
   critical, whole-flow confidence).
3. Record any acceptance criterion that could not be tested as
   written, and why — route back to `product-analyst` if the
   criterion itself is ambiguous.

## Exit criteria
Every acceptance criterion is either covered by a test or explicitly
flagged as untestable-as-written.

## Handoff
→ `code-review`; `devops-engineer` gates CI/CD on these tests passing.
