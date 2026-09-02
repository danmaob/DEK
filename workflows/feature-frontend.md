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
1. **For a new UI surface with no established direction** (added via
   incremental ECC extraction): establish it with
   `design-direction-and-system` before building — skip this step
   when extending an already-established design.
2. Type the API request/response shapes from the contract
   (`typescript-standards`).
3. Build components (`react-component-architecture`), wiring state
   per `frontend-state-management`.
4. Implement forms/validation (`forms-and-validation`) and API calls
   with explicit loading/error/success handling
   (`frontend-api-integration`).
5. Write component tests covering the acceptance criteria's happy path
   and at least one failure/edge case.
6. **Verify (added 0.1.1):** run the build, the linter/type-checker,
   and the full test suite before handoff. Include a
   `visual-design-quality-review` self-check (added via incremental
   ECC extraction) alongside this for any UI change, not just new
   surfaces.

## Exit criteria
Build, lint/type-check, and the full test suite all pass; each
acceptance criterion from the originating story is demonstrably met
and covered by a test.

## Handoff
→ `testing` (E2E if this is a critical flow), then `code-review` and,
if the UI handles user input or renders external content,
`security-review`.
