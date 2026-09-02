# Command: review-code

**Invokes:** `code-reviewer` (and `security-reviewer` when applicable)
**Use when:** a pull request/diff is ready for review.

## Instruction
1. Run `workflows/code-review.md` against the diff.
2. If the diff touches authentication, authorization, input handling,
   or data exposure, also run `workflows/security-review.md`.

## Output
Prioritized review comments (blocking/non-blocking) or an explicit
approval.
