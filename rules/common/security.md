# Rule: Security

- Never commit credentials, API keys, tokens, connection strings, or
  private keys to source control, including in examples or comments.
- Every endpoint that accepts input validates it server-side,
  regardless of any client-side validation.
- Every endpoint that returns tenant/user-scoped data checks
  authorization for that specific resource, not just authentication.
- All SQL is parameterized; string-concatenated queries built from
  user input are a blocking review finding.
- Logs never contain secrets, tokens, passwords, or full personal-data
  payloads.
- Any change to authentication, authorization, or how data is exposed
  externally requires a `security-review` pass before merge.
