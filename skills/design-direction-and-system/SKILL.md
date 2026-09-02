---
skill: design-direction-and-system
used_by: [frontend-engineer]
added_in: incremental ECC extraction (post-0.1.1)
source: ADAPT of ECC's skills/design-system/SKILL.md, "Mode 1:
  Generate Design System" and its competitor-research step
  (https://github.com/affaan-m/ECC — path confirmed via search/mirror,
  primary GitHub blob not directly fetchable in this environment; see
  UPDATE-MANIFEST.md for the sourcing note)
---

# Design Direction & Design System

Establishing a deliberate visual direction *before* building UI, and
keeping a consistent set of design tokens as the project grows. This
is a design-decision skill, not a frontend-implementation skill —
pair it with `react-component-architecture` and `typescript-standards`
for the actual build.

## When to use
- Starting a new project or a new significant UI surface that has no
  established visual direction yet.
- Before a UI redesign — understand what exists before changing it.
- When a new component needs a token/color/spacing decision and none
  of the existing ones clearly fit.

## Establish a direction, don't default to generic

Before writing any component, decide (briefly — a paragraph, not a
deck):
- **Visual personality**: what should this feel like — utilitarian
  and dense, calm and spacious, bold and confident? Pick one framing
  and let it guide decisions, rather than defaulting to whatever a
  component library ships with unmodified.
- **Hierarchy**: what should the eye land on first, second, third?
- **Typography direction**: a small number of weights/sizes with a
  clear purpose each (not "use whatever looks fine here").
- **Color direction**: a primary, a neutral scale, and a small set of
  semantic colors (success/warning/error) — not an ad hoc palette
  that grows one hex code at a time.
- **Spacing & layout character**: a consistent scale (e.g. a 4px or
  8px base unit), applied deliberately rather than picking arbitrary
  pixel values per component.

This is a DANMAOB/DEK design methodology, not a mandate to copy any
particular aesthetic — the *process* of deciding deliberately is the
transferable part, not any specific look.

## Look at comparable products first (lightweight)

Before finalizing a direction, look at 2-3 comparable products or
interfaces the team already knows or can quickly find — note what
works and what doesn't for this kind of product, and why. This is a
short, informal step (not a formal competitive-research exercise) —
the goal is informed decisions, not exhaustive research for every
task. Skip this step entirely for a small addition to an
already-established design.

## Design tokens

Once a direction is set, record it as explicit tokens rather than
letting values live only in component code:
- **Color**: primary, neutral scale, semantic (success/warning/error/
  info), each with light-mode (and dark-mode, if the project supports
  it) values.
- **Typography**: a small type scale (e.g. 5-7 sizes) with defined
  use (heading levels, body, caption) and a limited set of weights.
- **Spacing**: a consistent scale, not arbitrary per-component values.
- **Border radius, shadows/elevation**: a small, consistent set —
  usually 2-4 values cover a whole product.
- **Breakpoints**: the set of screen widths the product deliberately
  designs for, agreed once and reused everywhere.

Record tokens in whatever form the project's actual stack consumes
(CSS custom properties, a TypeScript theme object, or another
project-native mechanism) — don't introduce Tailwind, a specific
design-token tool, or any other technology the project doesn't
already use, just because it's a common way to implement this
elsewhere. Document the *values and rationale* in one short file the
team can reference (what each token is for, not just its value) —
this prevents the same color/spacing decision being re-litigated per
component.

## Component consistency & states

Similar elements should look and behave similarly across the product.
When adding a new component, check whether an existing token/pattern
already covers the need before introducing a new one-off value —
prefer reuse over a new variant that's 90% the same as something that
already exists.

## Handoff

Feeds `react-component-architecture` (implementation) and
`visual-design-quality-review` (the review/audit counterpart to this
skill — use that one when checking existing UI rather than
establishing a new direction).
