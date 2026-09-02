# Rule: C# / .NET Coding Standards

Always-follow standards for backend and mobile C# code, in addition to
`skills/csharp-coding-standards/SKILL.md`.

- Nullable reference types enabled; nullable warnings are fixed, not
  suppressed.
- Dependency injection for collaborators; no service-locator pattern,
  no unnecessary `static` mutable state.
- `async`/`await` for all I/O; no blocking calls (`.Result`, `.Wait()`)
  on async I/O paths.
- Every public API surface (controller, service interface) has a
  clear, single-sentence responsibility.

## Rule priority (added 0.1.1)
This file extends `rules/common/*.md` with stack-specific detail. Where
this file and a common rule genuinely conflict for this stack, this
file takes precedence — but that should be rare; check whether the
common rule was actually meant to allow an exception before assuming
a conflict.
