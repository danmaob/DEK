---
skill: visual-design-quality-review
used_by: [frontend-engineer, code-reviewer]
added_in: incremental ECC extraction (post-0.1.1)
source: ADAPT of ECC's skills/design-system/SKILL.md ("Mode 2: Visual
  Audit" and its AI-slop-flagging mode) and, narrowly, the "Design
  Quality"/"Originality"/"Craft" scoring language from
  skills/gan-style-harness/SKILL.md
  (https://github.com/affaan-m/ECC — see UPDATE-MANIFEST.md for the
  sourcing note)
---

# Visual Design Quality Review

A structured way to evaluate UI quality — useful when something looks
"off" but it's hard to say why, or as part of reviewing a PR that
touches styling. Pairs with `design-direction-and-system` (the
before-you-build counterpart) and with `frontend-testing-and-accessibility`
(which owns the testing/verification side of accessibility — this
skill covers the *design-quality* read, not a re-test of it).

## When to use
- The UI "feels off" but the specific problem isn't obvious yet.
- Reviewing a pull request that changes styling or adds new UI.
- Before a redesign, to understand what's actually there.

## Review dimensions

Score each roughly low/medium/high, or note pass/fail for a
lighter-weight review — the value is in checking every dimension
deliberately, not in a precise numeric score:

1. **Color consistency** — is the established palette (see
   `design-direction-and-system`) actually being used, or are new
   arbitrary values creeping in?
2. **Typography hierarchy** — is it clear at a glance what's a
   heading, subheading, body text, and caption?
3. **Spacing rhythm** — does spacing follow the agreed scale, or are
   values arbitrary per component?
4. **Component consistency** — do similar elements (buttons, cards,
   inputs) actually look and behave the same way across the product?
5. **Responsive behavior** — does the layout stay usable and
   intentional across breakpoints, or does it visibly break?
6. **Dark mode** (if the project supports it) — is it complete, or
   half-implemented in places?
7. **Animation/motion** — is motion purposeful (guiding attention,
   confirming an action) or gratuitous?
8. **Interaction states** — hover, focus, active, and disabled states
   are present and visually distinct; focus states are visible enough
   to support keyboard navigation (this overlaps with, but doesn't
   replace, the accessibility checks in
   `frontend-testing-and-accessibility`); touch targets are large
   enough on mobile/touch surfaces.
9. **Information density** — does the layout feel appropriately
   dense for its purpose, or cluttered/sparse without reason?
10. **Polish** — do transitions and hover/loading feedback feel
    deliberate, or is the interface visibly unfinished in places?

## Avoiding generic, templated interfaces

A UI can pass every dimension above and still feel generic and
interchangeable with any other AI-assisted or template-generated
product. Watch specifically for:
- Decoration with no purpose (a gradient, a shadow, or an icon that
  isn't communicating anything).
- Default component-library styling left completely unmodified when
  the product is meant to have its own identity.
- Layouts that default to the same card-grid/hero-section shape
  regardless of what the content actually needs.
- Typography and spacing that could belong to literally any product.
- Visual choices that don't obviously trace back to the direction set
  in `design-direction-and-system` — if there's no reason a decision
  was made, that's worth a second look.

The goal for DANMAOB's professional software products is a deliberate,
consistent identity — not a specific aesthetic mandated by this
skill. A plain, restrained interface that's consistent and clearly
intentional passes this check; a decorated interface with no
underlying rationale does not.

## Output

For a PR review, report findings the same way `code-review-checklist`
already does: prioritized, with a concrete fix, not a vague "improve
the visual design" comment. For a standalone audit, a short list of
findings per dimension above, with the highest-impact issues first,
is enough — this doesn't need a separate heavyweight report format.
