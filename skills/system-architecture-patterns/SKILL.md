---
skill: system-architecture-patterns
used_by: [architect]
---

# System Architecture Patterns

## Choosing a style
| Style | Fits when |
|---|---|
| Layered Architecture | Small-to-medium app, straightforward CRUD-heavy domain, team is small |
| Clean Architecture | Domain logic is non-trivial and needs to stay independent of frameworks/UI/DB |
| Vertical Slice | Features are largely independent; minimizing cross-feature coupling matters more than a shared domain layer |
| Modular Monolith | One deployable, but clear internal module boundaries anticipating a possible future split |

Pick the simplest style that satisfies the requirements' actual
complexity — do not default to Clean Architecture out of habit for a
small CRUD app, and do not default to a Layered Architecture for a
system with genuinely complex domain rules.

## Documenting the decision
Record the choice as an ADR
(`templates/architecture-decision-record-template.md`): context,
decision, alternatives considered, consequences. One ADR per
significant decision, not one giant "architecture" document that
tries to justify everything at once.

## Cross-cutting concerns to decide early
Authentication/authorization approach, logging/observability approach,
caching strategy (if any), and how errors surface to clients — deciding
these late causes rework across every layer.
