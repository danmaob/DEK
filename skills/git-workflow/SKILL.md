---
skill: git-workflow
used_by: [devops-engineer, all engineer agents]
---

# Git Workflow

## Branching
Feature branches off the main integration branch, named descriptively
(`feature/order-refunds`, `fix/null-ref-checkout`). Keep branches
short-lived — merge or close within days, not weeks, to limit drift.

## Commits
Small, focused commits with a clear message: a short imperative
summary line, then (if needed) a body explaining *why*, not just
*what* (the diff already shows what).

## Pull requests
Every non-trivial change goes through a PR using
`templates/pull-request-template.md`: what changed, why, how it was
tested, and any follow-up work called out explicitly. PRs get both a
`code-reviewer` pass and, when relevant, a `security-reviewer` pass
before merge.

## Anti-patterns
Force-pushing over a branch others are reviewing; committing generated
files, secrets, or large binaries into the repository.
