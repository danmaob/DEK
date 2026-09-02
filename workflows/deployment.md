# Workflow: Deployment

**Agent(s):** `devops-engineer`
**Skills:** `cicd-pipelines`, `git-workflow`
**Stage input:** Code that has passed `code-review` (and
`security-review` where required) and `testing`.
**Stage output:** A deployed change, with a recorded rollback path.

## Steps
1. Confirm CI is green (build, tests, lint, security scan gate).
2. Deploy to staging; run any required smoke checks.
3. Deploy to production behind an explicit approval step; have a
   rollback plan ready before deploying, not improvised after an
   incident.
4. Record the release (version, what changed) for `tech-writer`'s
   release notes.

## Exit criteria
The change is live in production, or explicitly rolled back with the
reason recorded.

## Handoff
→ `documentation-and-maintenance`.
