---
skill: secure-configuration-secrets
used_by: [security-reviewer, devops-engineer, backend-engineer]
---

# Secure Configuration & Secret Management

## Principles
- Secrets (connection strings, API keys, signing keys) never live in
  source control, including in example/sample config files — use
  placeholders there.
- Use environment-appropriate secret storage: user secrets locally,
  a managed secret store (e.g. platform key vault) in deployed
  environments.
- Separate configuration per environment (dev/staging/production);
  never point a non-production environment at production data or
  credentials.
- Disable verbose error pages, stack traces, and debug endpoints in
  production.
- Rotate secrets on a schedule and immediately after any suspected
  exposure.

## CI/CD
Inject secrets into pipelines via the CI platform's secret store, not
as plaintext pipeline variables committed to a config file.
