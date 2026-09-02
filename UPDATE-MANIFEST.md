# UPDATE-MANIFEST.md

## Baseline
DEK 0.1.1 (unchanged as a whole — this package modifies only the
specific files listed below within an existing DEK 0.1.1 installation).

## Source
ECC — `https://github.com/affaan-m/ECC`, current repository, analyzed
via targeted web search and individual file fetch (no `git clone`
available in this environment; see "Source fidelity note" below).

## Purpose
This is an incremental capability extraction/adaptation package for
an existing DEK 0.1.1 installation. It is **not** a new DEK version
and does not replace or rebuild DEK. It contains only the specific
ECC-derived capabilities requested for this task (product/UX
discovery and UI/UX design), copied when directly compatible and
adapted when ECC-specific assumptions didn't fit DEK.

## Source fidelity note
Every adopted capability below was traced to a specific ECC file and
verified with real, fetched content — not from memory or generic
knowledge of ECC. `commands/prp-prd.md` was fetched directly and in
full from GitHub (447 lines, complete content reviewed).
`skills/design-system/SKILL.md`, `skills/accessibility/SKILL.md`,
`skills/gan-style-harness/SKILL.md`, and `skills/browser-qa/SKILL.md`
were **not** successfully fetched directly from their GitHub blob URLs
in this session (the fetch tool available here can only reach a URL
already surfaced by a search or a prior fetch, and a direct fetch
attempt for one of these returned a permissions error before a usable
search result existed for it). Their content was instead reconstructed
from substantial, verbatim-quoted excerpts returned by web search —
directly from `github.com/affaan-m/ECC` search results in three of the
four cases (accessibility, gan-style-harness, browser-qa), and from
consistent excerpts across multiple independent third-party mirrors/
indexes of the same ECC file for design-system specifically (GitHub
search snippets, skills.sh, claudemarketplaces.com, api.airforce).
This is real ECC content — the excerpts include specific structural
detail (exact dimension lists, exact scoring language, exact
skill/file names) that would be very unlikely to appear consistently
across independent sources if fabricated — but it is a lower-confidence
sourcing method than a direct full-file fetch, and is flagged as such
per-capability below rather than presented as equivalent to the
prp-prd.md sourcing.

## Adopted capabilities

### 1. Evidence-based product discovery
- **ECC source**: `commands/prp-prd.md` ("Product Requirements
  Document Generator" — problem-first, hypothesis-driven PRD
  generator with foundation questions, evidence/assumption framing,
  MVP/non-goals, and a validation-status table)
- **Classification**: ADAPT
- **DEK artifact**: new `skills/evidence-based-product-discovery/SKILL.md`
  (new), new `templates/problem-brief-template.md` (new),
  `agents/product-analyst.md` (modified — skill reference + operating
  note)
- **Retained**: the problem-first ordering (Problem → User → Evidence
  → Goal → Proposed solution), the foundation questions (who/what/
  why/why-now/how-measured), the mandatory evidence-vs-assumption
  tagging discipline, the "write TBD rather than invent" anti-pattern,
  MVP/anti-goals/non-users framing, and the validation-status table.
- **Changed**: removed ECC's Claude-Code-specific mechanics entirely —
  the multi-phase interactive "GATE" question-set structure (which
  assumes one long, uninterrupted autonomous session), the
  `.claude/PRPs/prds/` output path, the `/prp-plan` and `/save-session`
  command integrations, and the market-research/technical-feasibility
  "grounding" phases that assume live codebase/browser tool access
  mid-conversation. Re-scoped as a skill `product-analyst` applies
  within DEK's existing file-based, one-stage-per-session model,
  explicitly positioned as a *complement* to (not a replacement for)
  DEK's existing `requirements-elicitation` skill, and reduced from
  ECC's full heavyweight PRD template (implementation phases, decision
  logs, parallelism notes) to a condensed `problem-brief-template.md`
  matching DEK's existing lightweight document style.

### 2. Design direction & design system
- **ECC source**: `skills/design-system/SKILL.md`, "Mode 1: Generate
  Design System" (codebase pattern scan → token extraction → light
  competitor research → token proposal → rationale doc). *Sourced
  from third-party mirror excerpts, cross-checked across independent
  sources — see "Source fidelity note" above.*
- **Classification**: ADAPT
- **DEK artifact**: new `skills/design-direction-and-system/SKILL.md`
  (new), `agents/frontend-engineer.md` (modified — skill reference +
  operating note), `workflows/feature-frontend.md` (modified — new
  step 1 for establishing direction on new UI surfaces)
- **Retained**: the principle of establishing a deliberate visual
  direction before implementation (personality, hierarchy, typography,
  color, spacing, layout character), the design-token categories
  (color/typography/spacing/radius/shadows/breakpoints), documenting
  rationale alongside values, and lightweight competitor/reference
  research before finalizing a direction.
- **Changed**: removed the mandate to output `DESIGN.md` +
  `design-tokens.json` + a self-contained interactive HTML preview
  page (ECC-specific artifact shapes); removed the "via browser MCP"
  tool dependency for competitor research, generalized to "look at 2-3
  comparable products, however you can"; explicitly instructed to
  record tokens in whatever mechanism the project's actual stack
  already uses rather than introducing Tailwind or any other specific
  technology, per DEK's stack-neutrality requirement for this task.

### 3. Visual design quality review
- **ECC source**: `skills/design-system/SKILL.md`, "Mode 2: Visual
  Audit" (10-dimension 0-10 scoring: color consistency, typography
  hierarchy, spacing rhythm, component consistency, responsive
  behavior, dark mode, animation, accessibility, information density,
  polish) and its "Mode 3" AI-slop flagging; narrowly, the
  Design-Quality/Originality/Craft scoring language from
  `skills/gan-style-harness/SKILL.md`. *Sourced from third-party
  mirror excerpts (design-system) and a GitHub search snippet
  (gan-style-harness) — see "Source fidelity note" above.*
- **Classification**: ADAPT
- **DEK artifact**: new `skills/visual-design-quality-review/SKILL.md`
  (new), `agents/frontend-engineer.md` and `agents/code-reviewer.md`
  (modified — skill references + operating notes),
  `workflows/feature-frontend.md` and `workflows/code-review.md`
  (modified — reference this skill during verify/review steps)
- **Retained**: all 10 audit dimensions (renamed "interaction states"
  to fold in ECC's "polish"/hover-state language plus a cross-reference
  to accessibility focus/touch-target checks, to avoid a duplicate
  11th dimension), the core anti-generic-design methodology (decoration
  with no purpose, unmodified default component-library styling,
  same-shape layouts regardless of content, generic typography/
  spacing), and the "report as findings with a concrete fix" review
  style.
- **Changed**: dropped ECC's specific branding ("AI slop," a numeric
  A-F grade system, a gamified $50-200 GAN-harness cost/investment
  framing) and reframed the underlying goal in DANMAOB's own
  professional-software-product language: a deliberate, consistent
  identity, evaluated qualitatively (low/medium/high or pass/fail)
  rather than with ECC's specific scoring apparatus, which assumes
  tooling DEK doesn't have. The numeric A-F grading and CI/CD gating
  described in secondary summaries of this skill were not adopted —
  DEK has no runtime to enforce a numeric gate.

### 4. Accessibility (enhancement to existing DEK skill)
- **ECC source**: `skills/accessibility/SKILL.md` (WCAG 2.2, POUR
  principles, semantic-element-before-ARIA preference, focus
  management, concrete contrast ratios) and `skills/browser-qa/SKILL.md`
  (the "automated tools cover ~30-40% of WCAG, a clean run is
  necessary but not sufficient" caveat). *Sourced from GitHub search
  snippets of these two files, not a direct full-file fetch — see
  "Source fidelity note" above.*
- **Classification**: ADAPT
- **DEK artifact**: `skills/frontend-testing-and-accessibility/SKILL.md`
  (modified — existing skill enhanced, not replaced or duplicated)
- **Retained**: the POUR framework, the native-semantics-before-ARIA
  principle, concrete contrast ratios (4.5:1 normal text, 3:1 large
  text), focus-order/focus-management guidance, and the "automated
  scan is a floor, not proof of accessibility" caveat with its real
  ~30-40% coverage figure.
- **Changed**: condensed from ECC's full Web+iOS+Android
  ARIA-trait-mapping mechanics into principles applicable across DEK's
  actual frontend (React/TypeScript) and mobile
  (.NET MAUI) stack, with an explicit pointer to
  `maui-architecture-and-platform` for MAUI-specific mechanics rather
  than duplicating platform API detail here. This is a modification of
  DEK's existing accessibility content per this task's explicit
  instruction not to duplicate DEK's existing testing capabilities —
  no new skill was created for this.

## Not adopted

- **B6. Responsive design, as a dedicated capability**: genuinely
  present in ECC (`skills/design-system/SKILL.md` dimension 5,
  `skills/browser-qa/SKILL.md` responsive testing phase) but only as
  one line item inside broader skills, not as a distinct ECC
  capability of its own. Folded as design-decision bullets into
  `skills/visual-design-quality-review/SKILL.md` (dimension 5) instead
  of creating a separate artifact — a dedicated file would duplicate
  content already covered there and in DEK's existing frontend
  engineering skills.
- **B9. Design references / competitive research, as a standalone
  capability**: real in ECC (`skills/design-system/SKILL.md` Mode 1,
  step 3) but thin enough, and tightly enough coupled to establishing
  a new direction, that it was folded into
  `skills/design-direction-and-system/SKILL.md` rather than given its
  own file.
- **C3. Feature prioritization**: ECC's `commands/prp-prd.md` reuses
  the same MoSCoW (Must/Should/Could/Won't) framework DEK's
  `estimation-prioritization` skill already has. Not genuinely
  complementary — already covered by DEK.
- **Non-DANMAOB-stack elements of `skills/design-system/SKILL.md`**:
  the specific `DESIGN.md`/`design-tokens.json`/HTML-preview output
  format, the browser-MCP tool dependency, and any Tailwind/Next.js/
  Figma/Storybook-specific mechanics referenced in mirrors of this
  skill — too ECC/tool-specific for a stack-neutral DEK artifact.
- **ECC's numeric A-F grading and CI/CD gating for design quality**
  (from secondary summaries of `skills/design-system/SKILL.md` and
  from `skills/gan-style-harness/SKILL.md`'s cost/investment framing):
  assumes tooling and a runtime gate DEK does not have; the underlying
  qualitative review dimensions were kept, the enforcement mechanism
  was not.

### Explicitly out of scope for this task (not investigated as
adoption candidates; excluded per instruction, not for lack of ECC
coverage)
- Information Architecture
- Wireframing
- Prototyping
- Usability Testing

If ECC contains incidental references to these (it does not appear to
have dedicated, named capabilities for any of them under
`affaan-m/ECC` specifically — a similarly-named `ux-principles` skill
that surfaces in search results for these terms belongs to a
different, unrelated author/repository and was correctly excluded
from consideration), they were not investigated further and no DEK
artifact was created for them. **Not sufficiently covered by ECC for
dedicated adoption** — and out of scope for this task regardless.

### A4. User Journey Analysis — **NOT SUFFICIENTLY COVERED BY ECC**
No dedicated ECC capability for user-journey mapping (current state /
future state / friction / time-to-value / prioritized UX
improvements) was found. `skills/browser-qa/SKILL.md` mentions
"critical user journeys" only in a QA-testing sense (verifying a
checkout/onboarding/search flow still works), not in a UX-analysis
sense. No artifact was created for this; nothing was invented to fill
the gap.

### A5. UX Before/After — **NOT SUFFICIENTLY COVERED BY ECC**
No dedicated ECC capability for describing current-vs-proposed UX,
interaction changes, or expected improvement was found as its own
concept. `skills/design-system/SKILL.md`'s audit-finding structure is
loosely related (it produces findings against a current state) but is
a quality-scoring exercise, not a before/after UX-change narrative —
promoting that loose relation into a dedicated "UX before/after"
artifact would have been exactly the kind of over-reach this task
warned against. No artifact was created for this.

## Future DEK capabilities
The following were investigated separately (prior to this task) and
are intentionally **not** implemented here. They are future DEK
capabilities to be designed independently, not ECC extraction targets:
- Information Architecture
- Wireframing
- Prototyping
- Usability Testing

No agents, skills, rules, workflows, commands, or templates were
created for any of these four areas in this package.

## Integration model
This package is intended to be copied into an existing DEK 0.1.1
installation:
- Files under `skills/`, `templates/` that are entirely new (see list
  above) can be copied in directly as new files.
- Files under `agents/`, `workflows/`, `skills/` that already exist in
  DEK 0.1.1 (`product-analyst.md`, `frontend-engineer.md`,
  `code-reviewer.md`, `discovery-and-requirements.md`,
  `feature-frontend.md`, `code-review.md`,
  `frontend-testing-and-accessibility/SKILL.md`) are provided here as
  **complete, ready-to-use replacement files** — each already contains
  the full original DEK 0.1.1 content plus the incremental addition,
  clearly marked "(added via incremental ECC extraction)" or
  "(added 0.1.1)" inline. Overwrite the corresponding file at the same
  path in the existing DEK 0.1.1 installation.
- No other DEK 0.1.1 file is touched by this package. Everything not
  listed above should be left exactly as it is.
