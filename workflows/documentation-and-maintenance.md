# Workflow: Documentation & Maintenance

**Agent(s):** `tech-writer` (documentation), `devops-engineer`
(maintenance)
**Skills:** `documentation-standards`
**Stage input:** A shipped feature/fix, or a scheduled maintenance
check.
**Stage output:** Updated project documentation; a maintenance log
entry for recurring housekeeping (dependency updates, config drift).

## Steps
1. Update the README/API docs/runbooks affected by the change.
2. Write release notes for the shipped change.
3. On a maintenance cadence (not tied to a specific feature): check
   for outdated dependencies with known vulnerabilities, review
   configuration drift between environments, and confirm backups/
   monitoring are still functioning as documented.

## Exit criteria
Documentation reflects actual current behavior; maintenance findings
are either resolved or explicitly scheduled.

## Handoff
Closes the loop back to `planning` for any follow-up work the
maintenance check surfaced.
