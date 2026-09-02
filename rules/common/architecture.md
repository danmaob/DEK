# Rule: Architecture

- The architecture style in effect for a project is decided once by
  `architect` and recorded as an ADR; do not silently introduce a
  different style in a new module without a new ADR.
- New code must respect existing module/layer boundaries. Reaching
  across a boundary that the architecture explicitly separates (e.g.
  UI calling the database directly) is a blocking review comment.
- Cross-cutting concerns (auth, logging, error handling, caching) use
  the project's established mechanism; do not introduce a second,
  parallel mechanism for the same concern.
- Prefer the simplest design that satisfies current, real
  requirements. Speculative generality for hypothetical future
  requirements is not justified by itself.
