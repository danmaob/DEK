# Workflow: Bug Fixing

**Agent(s):** Whichever engineer agent owns the affected layer;
`qa-engineer` for reproduction.
**Skills:** `dotnet-testing` / `frontend-testing-and-accessibility` /
`mobile-testing` as applicable.
**Stage input:** A bug report
(`templates/bug-report-template.md`).
**Stage output:** A fix with a regression test.

## Steps
1. Reproduce the bug with a failing test first — if it can't be
   reproduced, that itself is worth recording before further work.
2. Implement the minimal fix; avoid unrelated refactoring in the same
   change.
3. Confirm the regression test now passes and existing tests still
   pass.

## Exit criteria
A test exists that would have caught this bug, and it now passes.

## Handoff
→ `code-review`; `security-review` if the bug had any security
implication (e.g. an authorization bypass).
