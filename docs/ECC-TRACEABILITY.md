# ECC → DEK Traceability

This document records what DEK borrowed from "Everything Claude Code"
(ECC, `github.com/affaan-m/ECC`), and why, so future DEK maintenance
is possible when ECC changes. It is based on direct inspection of
ECC's public README (component catalog, "What's Inside" file tree, key
concepts section) as of the analysis date below — not on assumption.

**Analysis basis:** ECC's public README
(`github.com/affaan-m/ECC/blob/main/README.md`), which documents 68
agents, 284 skills, 94 command shims, a `rules/` directory split into
`common/` + per-language packs, a `hooks/` runtime, and a
plan → implement → review → verify methodology built around Claude
Code's plugin/hook system.

**Analysis date:** 2026-08-31 (README content as fetched on that
date; ECC is under active weekly development and may have changed).

## Classification key
- **KEEP** — concept adopted with no material change (re-expressed in
  plain Markdown, since DEK has no runtime).
- **ADAPT** — concept adopted but substantially reshaped for DANMAOB's
  single fixed stack and free-tier constraint.
- **REMOVE** — present in ECC, deliberately excluded from DEK.
- **CREATE** — present in DEK, with no equivalent needed in ECC.

| ECC component / concept | Classification | DEK destination | Rationale |
|---|---|---|---|
| Separation of agents / skills / rules / hooks as distinct concerns | KEEP | `agents/`, `skills/`, `rules/` (no hooks equivalent) | The separation of "always loaded" (rules) vs. "loaded on demand" (skills) vs. "scoped role" (agents) is sound and provider-independent; it is the main reason DEK stays small per turn. |
| plan → implement → review → verify loop | KEEP | `workflows/feature-backend.md`, `workflows/feature-frontend.md`, `workflows/feature-mobile.md` | The loop shape is generic engineering practice, not Claude-Code-specific. |
| Fresh-context code review as a distinct pass from implementation | KEEP | `agents/code-reviewer.md`, `workflows/code-review.md` | Reviewing from a fresh perspective catches more than the author re-reading their own work; this doesn't depend on any runtime. |
| Per-language reviewer/build-resolver agents (typescript-reviewer, go-reviewer, java-reviewer, kotlin-reviewer, rust-reviewer, cpp-reviewer, python-reviewer, etc. — 10+ language coverage) | ADAPT | `agents/backend-engineer.md`, `agents/frontend-engineer.md`, `agents/mobile-engineer.md`, `agents/database-engineer.md` | DEK targets one fixed stack, not 10+ languages, so the *pattern* (a dedicated engineer/reviewer role per major stack layer) is kept, collapsed to DANMAOB's four implementation layers instead of one agent per language. |
| TDD workflow (`tdd-workflow` skill, `tdd-guide` agent) with RED/GREEN/REFACTOR and hook-enforced evidence capture | ADAPT | `skills/dotnet-testing/SKILL.md`, `workflows/feature-backend.md`, `workflows/feature-frontend.md` | The RED/GREEN/REFACTOR loop is kept; the hook-enforced evidence capture is dropped because DEK has no runtime in 0.1.0 — evidence is just the tests themselves, committed. |
| Security scan (`/security-scan`, AgentShield static analysis) | ADAPT | `agents/security-reviewer.md`, `skills/security-checklist-owasp/SKILL.md`, `commands/security-scan.md`, `workflows/security-review.md` | The *checklist-driven review* concept is kept; the automated static-analysis tool (AgentShield) is replaced with an LLM-driven checklist review, since DEK ships no runtime/binary. |
| Rules split into `common/` + per-language packs, installed selectively | KEEP (structure) / ADAPT (content) | `rules/common/*`, `rules/csharp-dotnet/`, `rules/typescript-react/`, `rules/sql-server/`, `rules/dotnet-maui/` | Structure kept as-is (it directly supports "load only what a task needs"); content rewritten for DANMAOB's stack instead of ECC's TypeScript/Python/Go/Swift/PHP/ArkTS packs. |
| Commands as slash-command shims (`/plan`, `/code-review`, `/build-fix`, etc.) | ADAPT | `commands/*.md` | Kept as short, named entry points to a workflow, but written as plain instructions rather than a specific harness's slash-command syntax, so they work in any chat or agentic tool. |
| Business/content skills (`market-research`, `investor-materials`, `investor-outreach`, `article-writing`, `content-engine`) | ADAPT | `agents/product-analyst.md`, `skills/requirements-elicitation/SKILL.md`, `skills/user-stories-acceptance-criteria/SKILL.md`, `skills/estimation-prioritization/SKILL.md` | The general idea that an AI engineering team should cover business/product work, not just code, is kept; the specific ECC skills (aimed at fundraising/content marketing) are replaced with discovery/requirements/planning skills relevant to a client-services dev shop. |
| Hooks runtime (`hooks/hooks.json`, PreToolUse/PostToolUse/Stop events, memory-persistence, strategic-compact) | REMOVE | — | Requires a specific harness's runtime (Claude Code, Cursor, etc.); DEK 0.1.0 is a Markdown-only kit with no runtime dependency, by design (§2 exclusions in `DEK-SPEC.md`). |
| Multi-harness installers (`install.sh`, per-target profiles for Cursor/OpenCode/Gemini/Zed/Antigravity/Qwen/Kimi/etc.) | REMOVE | — | DEK is dropped into a project manually; an installer is out of scope for 0.1.0 and would need to track each harness's evolving plugin format, which conflicts with staying provider-agnostic. |
| Memory Vault / continuous-learning / instinct system | REMOVE | — | Depends on a persistent runtime and CLI (`ecc memory`, `ecc-universal`); DEK's equivalent durable-state mechanism is simply "save the workflow's output as a project file," which needs no tooling. |
| Language/framework coverage outside DANMAOB's stack (Go, Rust, PHP, Swift, Kotlin, HarmonyOS/ArkTS, PyTorch/ML pipelines, Django/Laravel/Spring/Quarkus packs, etc.) | REMOVE | — | Out of scope — DANMAOB's stack is SQL Server + C#/.NET/ASP.NET Core/EF Core + React/TypeScript + .NET MAUI; carrying unused coverage would work against "compact relative to ECC." |
| Orchestration tooling (`orch-*` agents, PM2 multi-service commands, GAN shell, Rust control-plane prototype) | REMOVE | — | Multi-agent/process orchestration is explicitly a paid/stronger-tier evolution path for DEK (`DEK-SPEC.md` §7.2, §14), not part of the free-tier-first 0.1.0 baseline. |
| SQL Server / T-SQL as a first-class specialization | CREATE | `agents/database-engineer.md`, `skills/sql-server-and-tsql/SKILL.md`, `rules/sql-server/coding-standards.md` | ECC has no SQL-Server-specific coverage (its database-reviewer agent targets generic/Supabase-style Postgres patterns); this is written new for DANMAOB. |
| ASP.NET Core / EF Core as a first-class specialization | CREATE | `agents/backend-engineer.md`, `skills/aspnet-core-patterns/SKILL.md`, `skills/ef-core-patterns/SKILL.md`, `skills/aspnet-core-cross-cutting-concerns/SKILL.md`, `rules/csharp-dotnet/coding-standards.md` | ECC's C#-adjacent coverage is limited to generic C# review; ASP.NET Core/EF Core-specific guidance is new. |
| .NET MAUI as a first-class specialization | CREATE | `agents/mobile-engineer.md`, `skills/maui-architecture-and-platform/SKILL.md`, `rules/dotnet-maui/coding-standards.md` | ECC has no mobile/MAUI coverage at all. |
| Free-tier operating discipline as an explicit, documented constraint | CREATE | `skills/free-tier-llm-operating-model/SKILL.md`, `DEK-SPEC.md` §7.1, §14 | ECC assumes a paid, hook-capable Claude Code runtime throughout; DANMAOB's "no paid LLM plan yet" constraint has no ECC equivalent and needed to be designed from scratch. |
| Handoff-based (file-artifact) agent coordination model, explicitly designed to require no live shared context between agents | CREATE | `DEK-SPEC.md` §14, every `workflows/*.md` "Handoff" section | ECC's coordination assumes a single running harness session and, in its multi-agent modes, live orchestration; DEK needed a coordination model that also works across separate, disconnected free-tier chat sessions. |

## Maintenance note
If ECC's structure changes materially in a future version, re-run this
comparison against the new README/file tree before assuming any row
above still holds — this table reflects ECC as analyzed on the date
above, not a live sync.

---

## 0.1.1 Deep-Review Addendum (2026-09-01)

This addendum documents a second, deeper ECC review performed for the
0.1.0 → 0.1.1 upgrade, reading individual ECC agent/skill/rule/command
files (not just the top-level README/catalog used for the table
above). See `BUILD-REPORT-0.1.1.md` for the honest coverage numbers —
this was a substantial, real review of ~18 individual documents, not
a claim of exhaustive coverage of ECC's 450+ files.

**Files actually opened and read in this pass:** `rules/README.md`
(full), `rules/common/` directory listing, `agents/code-reviewer.md`,
`agents/security-reviewer.md`, `agents/python-reviewer.md`,
`agents/tdd-guide.md`, `AGENTS.md`, `commands/code-review.md`,
`skills/golang-testing/SKILL.md`, `skills/django-tdd/SKILL.md`,
`skills/exa-search/SKILL.md`, `skills/blueprint/SKILL.md`,
`skills/ai-first-engineering/SKILL.md`, `skills/configure-ecc/SKILL.md`,
`skills/skill-comply/SKILL.md`.

| ECC finding | Classification | DEK destination | Rationale |
|---|---|---|---|
| `rules/README.md`'s explicit rule-priority convention (language/stack-specific rules override common rules where they genuinely conflict; each extends its common counterpart) | ADAPT | `rules/csharp-dotnet`, `rules/typescript-react`, `rules/sql-server`, `rules/dotnet-maui` (new "Rule priority" note in each) | DEK's 0.1.0 rules never stated precedence explicitly; this closes a real ambiguity at negligible cost. |
| `agents/code-reviewer.md`'s "Confidence-Based Filtering," evidence requirement for HIGH/CRITICAL findings, and "approve clean diffs" instruction | ADAPT | `agents/code-reviewer.md`, `skills/code-review-checklist/SKILL.md` | A concrete, well-tested discipline for keeping review signal-to-noise high; directly reduces wasted free-tier turns spent on low-value findings. |
| `agents/security-reviewer.md`'s "Initial Scan" (run available tooling first) and high-risk-area triage list | ADAPT | `agents/security-reviewer.md` | Cheap, concrete step that focuses limited review time; NuGet/npm equivalents substituted for ECC's npm-only examples. |
| `agents/security-reviewer.md` and `agents/code-reviewer.md`'s "Prompt Defense Baseline," present verbatim-ish across ECC's own most safety-critical agents | ADD | `rules/common/untrusted-content-and-prompt-safety.md` | A genuine gap in DEK 0.1.0: no guidance existed for agents handling pasted/fetched external content (tickets, logs, docs). Generalized to all agents, not just security-reviewer, and made provider-agnostic (ECC's version is Claude-Code-flavored). |
| `commands/code-review.md`'s "Phase 2 — CONTEXT" (read project rules and planning artifacts before the diff) | ADAPT | `workflows/code-review.md` (new "read context first" step) | Small process fix; reviewing without first loading the relevant rules/ADR wastes a review pass. |
| `agents/tdd-guide.md` + `skills/golang-testing/SKILL.md` + `skills/django-tdd/SKILL.md`, and a third-party (deepwiki) summary of `rules/common/development-workflow.md` describing that RED must be *confirmed* (test compiles and fails for the stated reason), not just written | ADAPT | `skills/dotnet-testing/SKILL.md` | DEK's 0.1.0 TDD loop already matched ECC's RED-GREEN-REFACTOR shape (KEEP, no change); this specific nuance — actually running and confirming the failure — was missing and is a common real mistake. Sourced partly from a secondary (non-ECC) summary; flagged as lower-confidence than the primary-source findings. |
| `skills/exa-search/SKILL.md`'s "drift-prone skill" framing (verify a tool/doc surface against current reality before relying on it) | ADAPT | `skills/free-tier-llm-operating-model/SKILL.md` (new "verify against current documentation" note) | Generalized beyond the specific Exa MCP tool to any framework/library/API detail an LLM might misremember or assume from a stale training cutoff. |
| `skills/blueprint/SKILL.md`'s 5-phase autonomous pipeline (Research → Design into PR-sized steps with a rollback strategy per step → ...) | ADAPT (narrow slice only) | `workflows/planning.md` (new "small, independently shippable increments" step) | Only the "size work into small, revertible increments" idea was adopted. The full pipeline — autonomous multi-phase execution with per-step model-tier assignment — was REJECTed as an orchestration/paid-tier concern out of scope for 0.1.1 (see below). |
| `skills/ai-first-engineering/SKILL.md`'s "Code Review in AI-First Teams" (review for behavior regressions/security/data-integrity/failure-handling/rollout-safety; minimize time on automatable style issues) | ADAPT | `skills/code-review-checklist/SKILL.md` (new "what to prioritize" section) | Independently confirms and sharpens the code-reviewer.md finding above; adopted together. |
| ECC's own "Start Using ECC" table naming `/save-session`, `/checkpoint`, and `/resume-session` as core, first-class workflows for ending/resuming a session | ADD | `commands/save-progress.md`, `templates/session-handoff-template.md` | DEK 0.1.0 already *claimed* a multi-session, free-tier-first operating model (`free-tier-llm-operating-model` skill, DEK-SPEC.md §7.1/§14) but gave it no concrete artifact. ECC treats session handoff as important enough to be a named, top-level workflow; DEK 0.1.0 only described the idea in prose. This closes that gap with one command + one template — no new agent or skill needed. |
| `AGENTS.md`'s agent list including `spec-miner` ("Brownfield spec extraction... onboarding brownfield projects to spec-driven development") | ADD (as a workflow, not a new agent) | `workflows/brownfield-onboarding.md`, plus a scope note in `agents/architect.md` | Genuine, concrete gap: DANMAOB, as a client-services shop, plausibly modifies existing systems at least as often as building new ones, and none of DEK 0.1.0's 12 workflows addressed onboarding to an under-documented existing system before designing a change. Implemented as a workflow assigning `architect` + `product-analyst` rather than a 12th agent, since the work fits their existing responsibilities. |
| `skills/skill-comply/SKILL.md` (automated LLM-driven compliance measurement for whether an agent actually follows a skill/rule) | REJECT | — | Requires a runnable harness/CLI (`uv run python -m scripts.run ...`) and live model calls to grade compliance — out of scope for a Markdown-only kit with no runtime. |
| `agents/python-reviewer.md`'s language-specific review priorities | REJECT (as a file) / catalog-confirms decision already made | — | Python is outside DANMAOB's stack; confirms the existing 0.1.0 REMOVE decision for non-stack language reviewers rather than changing anything. |
| `skills/configure-ecc/SKILL.md`'s interactive installer/configuration wizard concept | REJECT | — | Assumes a CLI/installer runtime DEK deliberately does not have (§2 exclusions, DEK-SPEC.md). |
| `skills/exa-search/SKILL.md`'s specific MCP tool integration | REJECT (as a tool integration) / ADAPT (underlying idea only, see above) | — | The specific Exa MCP server is a paid third-party tool; only the generalizable "verify before relying on a drift-prone external surface" principle was kept. |
| `skills/blueprint/SKILL.md`'s autonomous multi-phase pipeline and per-step model-tier assignment | REJECT (as a whole) | — | Assumes autonomous, unattended multi-step execution and the ability to route different steps to different model strengths — both squarely paid/orchestration-tier concerns per DEK-SPEC.md §7.2, not part of the free-tier-first 0.1.1 baseline. |
| `AGENTS.md`'s `chief-of-staff`, `loop-operator`, `harness-optimizer` agents | REJECT | — | Communication-triage, autonomous-loop-monitoring, and harness-config-tuning roles assume a persistent runtime/harness (Claude Code specifically for the latter two) with no DEK equivalent and no clear DANMAOB use case. |

## Maintenance note (0.1.1)
This addendum reflects ECC as analyzed on 2026-09-01, at the depth
described in `BUILD-REPORT-0.1.1.md`. A future review should read
further into ECC's remaining files (particularly `hooks/`, `scripts/`,
and the per-language `rules/` packs not touched here) before assuming
this addendum is complete, and should append rather than overwrite.
