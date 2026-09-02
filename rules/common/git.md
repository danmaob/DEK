# Rule: Git

- Work happens on short-lived, descriptively named feature branches;
  no direct commits to the main integration branch.
- Every non-trivial change goes through a pull request with a filled
  `templates/pull-request-template.md` and at least one `code-review`
  pass before merge.
- Commit messages: an imperative summary line, plus a body explaining
  *why* when the *what* isn't obvious from the diff.
- No secrets, generated build artifacts, or large binaries are
  committed to the repository.
