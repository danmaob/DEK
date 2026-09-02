# Workflow: Architecture & Design

**Agent(s):** `architect` (consulting `database-engineer` on schema)
**Skills:** `system-architecture-patterns`, `api-design`,
`sql-server-and-tsql`
**Stage input:** Prioritized stories from `planning`.
**Stage output:** An architecture note/ADR, an API contract sketch,
and a database design brief.

## Steps
1. `architect` chooses (or confirms) the architectural style for this
   piece of work (`system-architecture-patterns`).
2. Sketch the API contract for any new/changed endpoints
   (`api-design`, `templates/api-endpoint-spec-template.md`).
3. Draft the database design brief; hand off to `database-engineer`
   for schema/indexing detail (`sql-server-and-tsql`).
4. Record any significant decision as an ADR
   (`templates/architecture-decision-record-template.md`).
5. If the design touches authentication, authorization, or external
   data exposure, route it to `security-review` before implementation
   starts.

## Exit criteria
An engineer agent could start implementation without needing to make
another architectural decision mid-task.

## Handoff
→ `feature-backend`, `feature-frontend`, `feature-mobile` as applicable.
