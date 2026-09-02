---
skill: frontend-api-integration
used_by: [frontend-engineer, mobile-engineer]
---

# Frontend/Mobile API Integration

## Principles
- Centralize API calls behind a typed client layer instead of
  scattering raw fetch/HTTP calls through components/views.
- Handle three states explicitly for every request: loading, error,
  success — never assume success.
- Map API error responses (see `api-design`) to user-facing messages
  that don't leak internal details.
- Retry transient network failures with backoff where it makes sense
  (mobile especially); don't silently retry non-idempotent requests
  (e.g. POST that creates a resource) without care.

## Authentication
Attach auth tokens through a single interceptor/handler rather than
per-call; handle token expiry/refresh in one place so every screen
benefits automatically.

## Offline / connectivity (mobile-relevant)
Detect connectivity loss and surface it to the user rather than
letting requests fail silently or hang indefinitely.
