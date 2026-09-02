---
skill: api-design
used_by: [architect, backend-engineer]
---

# API Design

## Principles
- Resource-oriented URLs (`/orders/{id}`, not `/getOrder?id=`).
- Use HTTP status codes correctly: 200/201/204 for success variants,
  400 for client input errors, 401/403 for auth, 404 for missing
  resources, 409 for conflicts, 422 for validation failures, 5xx only
  for genuine server faults.
- Consistent envelope for errors: an error code, a human-readable
  message, and (for validation) a per-field detail list.
- Version explicitly (URL segment or header) once a breaking change is
  needed — don't silently change a shipped contract.

## Pagination
Prefer cursor-based pagination for large or frequently-changing
collections; offset/limit is acceptable for small, stable ones. Always
cap page size server-side.

## Documenting a contract
Use `templates/api-endpoint-spec-template.md` per endpoint: method,
path, auth requirement, request shape, response shape (success and
error), and status codes. This is what `frontend-engineer` and
`mobile-engineer` implement against, so ambiguity here becomes rework
later.

## Anti-patterns
- Returning 200 with an error payload inside the body.
- Leaking internal exception messages or stack traces to clients.
