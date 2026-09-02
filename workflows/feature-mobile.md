# Workflow: Feature Development — Mobile (.NET MAUI)

**Agent(s):** `mobile-engineer`
**Skills:** `maui-architecture-and-platform`, `csharp-coding-standards`,
`frontend-api-integration`
**Stage input:** API contract from `architecture-design`.
**Stage output:** Merged, tested mobile feature code.

## Steps
1. Decide MVVM vs. lightweight code-behind based on the screen's
   actual interactivity (`maui-architecture-and-platform`).
2. Implement navigation, data binding, and API integration
   (`frontend-api-integration`).
3. Handle permissions, offline/connectivity, and platform differences
   explicitly.
4. Write tests for view models and platform-agnostic logic
   (`mobile-testing`, in the `testing` workflow).
5. **Verify (added 0.1.1):** run a full build for both platforms and
   the full test suite before handoff.

## Exit criteria
Both platform builds and the full test suite pass; the feature works
correctly on both iOS and Android for the primary scenario, and
degrades gracefully (not silently) when offline or when a permission
is denied.

## Handoff
→ `testing` (device/emulator pass), then `code-review` and, if the
feature touches local storage/permissions/tokens, `security-review`.
