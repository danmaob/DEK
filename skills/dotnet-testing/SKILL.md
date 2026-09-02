---
skill: dotnet-testing
used_by: [qa-engineer, backend-engineer]
---

# .NET Testing (Unit & Integration)

## Unit tests
Test one unit of behavior per test; name tests to describe behavior
(`Returns404_WhenOrderDoesNotExist`, not `Test1`). Mock external
dependencies (HTTP clients, repositories) at the boundary; don't mock
the thing under test.

## Integration/API tests
Use `WebApplicationFactory` (or equivalent) to test the real ASP.NET
Core pipeline against a real or test database (a disposable
container/local test DB, not a shared dev database). Cover
authentication/authorization behavior, not just happy-path responses.

## TDD loop
1. Write a failing test that expresses the desired behavior (RED).
2. **Actually run it and confirm it fails for the expected reason**
   (added 0.1.1) — a test that fails to compile, or fails for the
   wrong reason, isn't a valid RED state and doesn't prove anything
   once you make it pass.
3. Write the minimal code to pass it (GREEN).
4. Refactor with the test as a safety net (REFACTOR).
Repeat per behavior, not per class.

## Coverage
Aim for meaningful coverage of business logic and edge cases;
100% coverage of trivial getters/DTOs is not a useful goal.
