# Workflow: Feature Development — Frontend

**Agent(s):** `frontend-engineer`
**Skills:** `react-component-architecture`, `typescript-standards`,
`frontend-state-management`, `forms-and-validation`,
`frontend-api-integration`
**Stage input:** API contract from `architecture-design` (or the
already-implemented backend endpoint).
**Stage output:** Merged, tested UI implementing the story's
acceptance criteria.

## Steps
1. Type the API request/response shapes from the contract
   (`typescript-standards`).
2. Build components (`react-component-architecture`), wiring state
   per `frontend-state-management`.
3. Implement forms/validation (`forms-and-validation`) and API calls
   with explicit loading/error/success handling
   (`frontend-api-integration`).
4. Write component tests covering the acceptance criteria's happy path
   and at least one failure/edge case.
5. **Verify (added 0.1.1):** run the build, the linter/type-checker,
   and the full test suite before handoff.

## Exit criteria
Build, lint/type-check, and the full test suite all pass; each
acceptance criterion from the originating story is demonstrably met
and covered by a test.

## Handoff
→ `testing` (E2E if this is a critical flow), then `code-review` and,
if the UI handles user input or renders external content,
`security-review`.
