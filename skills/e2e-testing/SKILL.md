---
skill: e2e-testing
used_by: [qa-engineer]
---

# End-to-End Testing

## When E2E is justified
For the small number of flows where end-to-end confidence is worth
the higher maintenance cost: login, checkout/payment, and any flow
whose failure would be a severe business incident. Not every user
story needs an E2E test.

## Practices
- Test through the UI as a real user would, against a real (test)
  backend and database, not mocks.
- Use stable selectors (test IDs) rather than brittle text/CSS
  selectors that break on copy or style changes.
- Keep E2E suites small and fast enough to run in CI without becoming
  a bottleneck; push edge-case coverage down to unit/integration tests
  instead of growing the E2E suite indefinitely.

## Anti-patterns
Using E2E tests to cover logic that a unit or integration test could
verify faster and more reliably.
