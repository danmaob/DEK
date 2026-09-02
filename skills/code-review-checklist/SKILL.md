---
skill: code-review-checklist
used_by: [code-reviewer]
---

# Code Review Checklist

- Does the change do what the PR description/linked story says, and
  nothing unrelated?
- Is naming clear enough that a comment isn't needed to explain intent?
- Is error handling present for the failure paths that matter (not
  just the happy path)?
- Are there tests, and do they actually exercise the new behavior
  (not just re-assert a mock)?
- Does the change follow the relevant stack-specific rules file
  (`rules/csharp-dotnet`, `rules/typescript-react`, `rules/sql-server`,
  `rules/dotnet-maui`)?
- Is there duplicated logic that should be extracted, without
  over-abstracting a single occurrence into a premature framework?
- Does the change match the agreed architecture/API contract, or is
  the contract now out of date and needs an ADR update?

## Style of feedback
Prioritize comments as blocking vs. non-blocking; give a concrete
suggestion, not just a criticism.

## What to prioritize (added 0.1.1)
Spend review time on what tooling can't already catch: behavior
regressions, incorrect security/authorization assumptions, data
integrity risks, missing failure-path handling, and rollout/rollback
safety. Minimize time on style/formatting issues a linter or formatter
already enforces automatically — flag those only if no such tool is
configured for this project yet.

## Common false positives to skip
- "Add error handling" on a call whose failure path is already handled
  by a caller, a global exception-handling middleware, or a framework
  default (see `aspnet-core-cross-cutting-concerns`) — check the
  actual call chain before flagging this.
- Restating a project convention that's already enforced by an
  analyzer/linter/formatter in this repo.
