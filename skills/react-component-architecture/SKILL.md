---
skill: react-component-architecture
used_by: [frontend-engineer]
---

# React Component Architecture

## Composition
Prefer small, single-purpose components over large ones with many
conditional branches. Lift state up only as far as it needs to go —
not automatically to the top of the tree.

## Structure
Group files by feature (a feature folder with its components, hooks,
and types) rather than by file type (a global `components/`,
`hooks/`, `types/`) once the app grows past a handful of screens.

## Hooks
Extract repeated stateful logic into custom hooks; keep hooks focused
on one concern (`useOrderStatus`, not `useEverything`).

## Anti-patterns
- Prop drilling more than two or three levels — consider context or a
  state management solution instead.
- Components that both fetch data and render complex presentation —
  split fetching/orchestration from presentation where it aids testing.
- Re-implementing behavior the platform or a well-established library
  already provides correctly (focus traps, date parsing, etc.).
