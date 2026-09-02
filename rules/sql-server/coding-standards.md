# Rule: SQL Server Coding Standards

Always-follow standards for schema and T-SQL, in addition to
`skills/sql-server-and-tsql/SKILL.md`.

- Every table has an explicit primary key and appropriate foreign key
  constraints.
- All queries built with user input are parameterized; no dynamic SQL
  built via string concatenation of untrusted input.
- Every schema change ships as a reviewed migration script, never as
  an untracked direct change to a shared environment.
- New frequently-queried columns are evaluated for indexing before the
  change is considered complete.

## Rule priority (added 0.1.1)
This file extends `rules/common/*.md` with stack-specific detail. Where
this file and a common rule genuinely conflict for this stack, this
file takes precedence — but that should be rare; check whether the
common rule was actually meant to allow an exception before assuming
a conflict.
