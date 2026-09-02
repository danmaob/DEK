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

## Deeper principles (added via incremental ECC extraction)
Source: ADAPT of ECC's skills/accessibility/SKILL.md and
skills/browser-qa/SKILL.md.

- **POUR**: every check above exists to make the interface
  Perceivable, Operable, Understandable, and Robust. When something
  doesn't fit the basics list above, ask which of these four it's
  failing — it usually clarifies what "accessible" actually means for
  that specific case.
- **Prefer native semantics over custom ARIA.** Use the actual
  semantic element (`<button>`, `<nav>`, `<label>`) before reaching
  for a generic `<div>` plus ARIA roles — native elements carry
  built-in keyboard and screen-reader behavior that a re-implemented
  custom control has to earn back manually.
- **Concrete contrast targets**: 4.5:1 for normal text, 3:1 for large
  text (roughly 18px+ or 14px+ bold) — check actual computed contrast,
  not just "looks readable."
- **Focus management**: keyboard/screen-reader focus order should
  match visual/logical order, and moving focus programmatically
  (opening a modal, submitting a form) should land somewhere sensible,
  not silently stay put or jump to the top of the page.
- **An automated pass is necessary, not sufficient.** Tools like axe
  cover roughly 30-40% of WCAG success criteria — a clean automated
  run does not mean "accessible." Keyboard navigation, focus order,
  and a screen-reader spot check still need a manual pass on new or
  complex UI before calling it done.
- This applies to mobile (`.NET MAUI`) too: platform accessibility
  traits (accessible labels, hints, and focus order equivalents on
  iOS/Android) follow the same principles as web ARIA — see
  `maui-architecture-and-platform` for platform-specific mechanics.
