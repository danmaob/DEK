# Workflow: Feature Development — Backend (incl. Database Changes)

**Agent(s):** `database-engineer` (schema), `backend-engineer`
(implementation)
**Skills:** `sql-server-and-tsql`, `ef-core-patterns`,
`aspnet-core-patterns`, `csharp-coding-standards`,
`aspnet-core-cross-cutting-concerns`, `authentication-authorization`,
`dotnet-testing`
**Stage input:** Architecture note, API contract, database design
brief from `architecture-design`.
**Stage output:** Merged, tested backend code implementing the
contract.

## Steps
1. `database-engineer` implements/migrates the schema per the design
   brief, with indexing considered up front.
2. `backend-engineer` writes a failing test expressing the desired
   endpoint/business-logic behavior (RED).
3. Implement the minimal code to pass it (GREEN), then refactor
   (REFACTOR) — see `dotnet-testing`.
4. Wire authentication/authorization per `authentication-authorization`.
5. Confirm the implementation matches the API contract exactly; note
   and escalate any deliberate deviation.
6. **Verify (added 0.1.1):** run a full build, the linter/formatter,
   and the full test suite (not just the new tests) before handoff —
   catching a break here is cheaper than catching it in `code-review`
   or CI.

## Exit criteria
Build, lint, and the full test suite all pass; the endpoint matches
the agreed contract; no known TODOs blocking correctness remain
unflagged.

## Handoff
→ `testing` (broader test strategy pass), then `code-review` and, for
anything touching auth/input/data exposure, `security-review`.
