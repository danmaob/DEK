---
skill: authentication-authorization
used_by: [backend-engineer, architect, security-reviewer]
---

# Authentication & Authorization

## Authentication
Prefer standard, well-reviewed mechanisms (e.g. JWT bearer tokens via
ASP.NET Core's built-in authentication middleware, or an established
identity provider) over hand-rolled schemes. Store password hashes
with a modern algorithm (e.g. ASP.NET Core Identity's default) — never
store or log plaintext passwords.

## Authorization
Authorize at the endpoint/handler level (`[Authorize]`, policy-based
authorization) and check ownership/tenancy explicitly for any resource
that is user- or tenant-scoped — authentication alone does not imply
the caller may access a specific record.

## Tokens & secrets
Keep token lifetimes short where practical; use refresh tokens with
rotation rather than very long-lived access tokens. Never place
secrets, connection strings, or keys directly in source control —
reference them from configuration/secret storage.

## Review checklist
Every new endpoint should answer: does it require authentication?
does it check authorization for the specific resource? is the
check enforced server-side (never trust a client-side check alone)?
