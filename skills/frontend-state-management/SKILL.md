---
skill: frontend-state-management
used_by: [frontend-engineer]
---

# Frontend State Management

## Decision guide
| Situation | Approach |
|---|---|
| State used by one component and its direct children | Local component state |
| State shared across a few nearby components | Lift state to their common parent |
| State needed broadly across the app (auth, theme) | React context |
| Complex, frequently-updated shared state, or state needing time-travel/devtools | A dedicated state library |
| Server data (API responses) | A data-fetching/caching layer, not manually copied into global state |

## Principles
Keep server state and client UI state conceptually separate — don't
copy fetched data into a global store just to avoid prop drilling;
solve prop drilling with composition or context, and cache server data
with a fetching layer that already handles staleness/refetching.

## Anti-patterns
Introducing a heavyweight state library before local state and context
have actually become unmanageable.
