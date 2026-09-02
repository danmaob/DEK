# Rule: Documentation

- A change that alters externally-visible behavior (API contract, UI
  flow, CLI/config surface) updates the relevant documentation in the
  same change, not as a follow-up that may never happen.
- Significant architecture decisions are recorded as ADRs at the time
  they're made, not reconstructed later from memory.
- Documentation states current behavior only; remove or clearly mark
  content describing a previous version's behavior.
