# Rule: Testing

- New behavior ships with a test that would fail without it.
- Bug fixes ship with a regression test reproducing the bug.
- Tests assert observable behavior, not implementation details;
  refactoring without behavior change should not break tests.
- No numeric coverage percentage is enforced by itself — coverage of
  trivial code is not a substitute for coverage of business logic and
  edge/failure paths.
- Flaky tests are fixed or removed, not silently re-run until green.
