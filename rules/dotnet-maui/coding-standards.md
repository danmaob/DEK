# Rule: .NET MAUI Coding Standards

Always-follow standards for mobile code, in addition to
`skills/maui-architecture-and-platform/SKILL.md`.

- Sensitive data (tokens, credentials) uses secure storage, never
  plain preferences or files.
- Platform-specific branches are isolated behind an abstraction, not
  scattered `#if` blocks through shared logic.
- Every feature that uses a device permission handles the
  denied/revoked case explicitly.
- Network-dependent actions check connectivity and degrade gracefully
  when offline.

## Rule priority (added 0.1.1)
This file extends `rules/common/*.md` with stack-specific detail. Where
this file and a common rule genuinely conflict for this stack, this
file takes precedence — but that should be rare; check whether the
common rule was actually meant to allow an exception before assuming
a conflict.
