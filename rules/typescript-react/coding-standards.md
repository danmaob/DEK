# Rule: TypeScript / React Coding Standards

Always-follow standards for frontend code, in addition to
`skills/typescript-standards/SKILL.md` and
`skills/react-component-architecture/SKILL.md`.

- `strict` TypeScript mode on; no unexplained `any` or `@ts-ignore`.
- API response/request shapes are explicitly typed and kept in sync
  with the backend contract.
- Components handle loading/error/success states explicitly for any
  data they fetch.
- No secrets or API keys embedded in frontend code or bundled assets.

## Rule priority (added 0.1.1)
This file extends `rules/common/*.md` with stack-specific detail. Where
this file and a common rule genuinely conflict for this stack, this
file takes precedence — but that should be rare; check whether the
common rule was actually meant to allow an exception before assuming
a conflict.
