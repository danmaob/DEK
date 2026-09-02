---
skill: documentation-standards
used_by: [tech-writer]
---

# Documentation Standards

## What belongs where
- **README**: what the project is, how to run it locally, how to run
  tests — kept current, kept short.
- **ADRs**: significant architecture decisions, one file per decision.
- **API docs**: per-endpoint contract (see `templates/api-endpoint-spec-template.md`),
  generated or hand-maintained but always matching actual behavior.
- **Runbooks**: operational steps for deployment, rollback, and common
  incident response.

## Principles
Write for a reader who has none of the author's current context.
Prefer accurate and short over exhaustive and stale — update
documentation as part of the change that makes it inaccurate, not as
a separate cleanup pass that never happens.

## Anti-patterns
Auto-generating large documentation files that restate the code
without adding explanatory value; letting docs describe a previous
version of the behavior.
