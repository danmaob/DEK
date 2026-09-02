---
skill: cicd-pipelines
used_by: [devops-engineer]
---

# CI/CD Pipelines

## Minimum pipeline stages
1. Restore/build.
2. Run unit + integration tests; fail the build on any failure.
3. Lint/format check.
4. Security scan gate (dependency vulnerabilities at minimum).
5. Build deployable artifact.
6. Deploy to a staging/test environment automatically; deploy to
   production behind an explicit approval step.

## Principles
Keep the pipeline fast — slow pipelines get bypassed. Fail fast (cheap
checks like lint before expensive ones like E2E tests). Make pipeline
failures actionable: the log should tell the next engineer what broke
and why, not just "build failed."

## Deployment
Prefer deployments that support quick rollback (blue/green, or a
documented rollback script) over one-way migrations with no fallback,
especially for database changes — pair risky schema changes with a
backward-compatible rollout when possible.
