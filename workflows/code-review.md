# Workflow: Code Review

**Agent(s):** `code-reviewer`
**Skills:** `code-review-checklist`, plus the relevant stack skill(s)
**Stage input:** A pull request / diff.
**Stage output:** Prioritized review comments, or approval.

## Steps
1. Read context first (added 0.1.1): the relevant `rules/` files for
   this stack, any ADR or API contract the change should match, and
   the PR description/linked story or bug for stated intent — before
   reading the diff line by line.
2. Confirm the change matches that stated intent and nothing unrelated
   snuck in.
3. Work through `code-review-checklist`, applying its confidence-based
   filtering — don't report low-confidence or purely stylistic issues.
4. Prioritize comments as blocking vs. non-blocking; every blocking
   comment needs the evidence `code-review-checklist` requires
   (snippet, failure scenario, why existing guards don't catch it).
5. Re-review after the author addresses blocking comments. If the diff
   is clean, approve it.

## Exit criteria
No open blocking comments.

## Handoff
→ `deployment` (via `devops-engineer`), once `security-review` has
also signed off for changes that needed it.
