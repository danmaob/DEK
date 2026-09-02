---
skill: csharp-coding-standards
used_by: [backend-engineer, mobile-engineer, code-reviewer]
---

# C# Coding Standards

- Use `PascalCase` for types/methods/public members,
  `camelCase` for locals/parameters, `_camelCase` for private fields.
- Prefer immutability: `readonly` fields, records for DTOs/value
  objects, avoid unnecessary mutable shared state.
- Use nullable reference types (`#nullable enable`) and treat warnings
  as signal, not noise to suppress.
- Prefer explicit types when clarity matters, `var` when the type is
  obvious from the right-hand side.
- One class's public responsibility should be describable in one
  sentence; if it needs "and," consider splitting it.
- Use dependency injection for collaborators; avoid `static` state and
  service locators, which make testing and reasoning harder.
- Catch specific exception types; never swallow an exception silently —
  log or rethrow with context.
