---
skill: typescript-standards
used_by: [frontend-engineer, code-reviewer]
---

# TypeScript Standards

- Avoid `any`; use `unknown` plus a type guard when the type is
  genuinely not known yet.
- Model API responses with explicit types/interfaces generated or
  hand-written from the API contract in `templates/api-endpoint-spec-template.md`
  — don't let response shapes drift silently.
- Prefer `type` for unions/utility compositions, `interface` for
  object shapes meant to be extended.
- Enable `strict` mode; treat a growing list of `// @ts-ignore` as a
  signal that types need fixing, not suppressing.
- Use discriminated unions for state that has meaningfully different
  shapes per case (e.g. `{ status: 'loading' } | { status: 'error', error } | { status: 'success', data }`)
  instead of many optional fields with unclear validity combinations.
