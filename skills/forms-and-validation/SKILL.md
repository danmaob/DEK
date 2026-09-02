---
skill: forms-and-validation
used_by: [frontend-engineer]
---

# Forms & Validation

## Principles
- Validate on the client for immediate feedback, but never trust
  client-side validation alone — the server must validate again
  (see `aspnet-core-patterns`).
- Show field-level errors next to the field, plus a form-level summary
  for accessibility (screen readers benefit from both).
- Disable submit while a request is in flight; show a clear pending
  state; handle both validation errors (422) and unexpected errors
  (5xx) distinctly.

## Structure
Prefer a form library or a small set of reusable hooks over
hand-rolling validation logic per form once a project has more than a
couple of forms — consistency matters more than the specific library
chosen.

## Anti-patterns
- Silent failures (a submit button that does nothing when validation
  fails, with no visible error).
- Re-validating the entire form on every keystroke in a way that
  causes visible lag on large forms.
