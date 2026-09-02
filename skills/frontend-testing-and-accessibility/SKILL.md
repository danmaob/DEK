---
skill: frontend-testing-and-accessibility
used_by: [qa-engineer, frontend-engineer]
---

# Frontend Testing & Accessibility

## Component tests
Test components through their rendered output and user interactions
(click, type, submit), not through internal implementation details —
this keeps tests stable across refactors.

## What to test
- Happy path rendering with representative data.
- Loading and error states.
- Form validation feedback.
- Conditional rendering logic (permissions, feature flags).

## Accessibility basics
- Every interactive element is reachable and operable by keyboard.
- Images have meaningful `alt` text (or empty `alt` for purely
  decorative ones).
- Form fields have associated labels.
- Color is never the only way information is conveyed.
- Run an automated accessibility check (e.g. axe) as a baseline; treat
  it as a floor, not a substitute for manual keyboard/screen-reader
  spot checks on new, complex UI.
