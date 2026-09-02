# Rule: Error Handling

- Every failure path a user or caller can realistically hit is
  handled explicitly — no silently swallowed exceptions.
- Internal exception details (stack traces, raw exception messages)
  never reach an external client; translate them into the project's
  standard error response shape.
- Errors are logged with enough context (correlation ID, relevant
  identifiers) to diagnose without secrets or personal data in the
  log line.
- Distinguish expected failure (validation error, not-found) from
  unexpected failure (bug, infrastructure fault) in both status code
  and logging severity.
