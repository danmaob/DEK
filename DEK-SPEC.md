# DEK-SPEC.md — DANMAOB Engineering Kit Specification

Version: **0.1.1**
Status: Source of truth for the current DEK implementation. This spec
carries forward from 0.1.0 with targeted updates only (§10–§13); see
`BUILD-REPORT-0.1.1.md` for what changed and why.

---

## 1. Purpose

DEK (DANMAOB Engineering Kit) is DANMAOB's own AI Software Engineering
Team: a coordinated set of role definitions (agents), reusable knowledge
modules (skills), staged processes (workflows), always-on standards
(rules), short repeatable operations (commands), and reusable document
templates. It lets DANMAOB run real software projects — from business
discovery through architecture, implementation, testing, security,
review, deployment, documentation, and maintenance — with any capable
LLM, starting on free-tier plans.

DEK is **not** a smaller copy of "Everything Claude Code" (ECC). ECC is
reference material: a large, Claude-Code-specific agent harness (68
agents, 284 skills, 94 commands, hooks, and orchestration tooling).
DEK selectively borrows the *engineering ideas* behind ECC's components
— what a code reviewer should check, how a TDD loop should run, how
rules should be scoped — and re-expresses them as plain Markdown that
any chat-based or agentic LLM can read and follow, without hooks,
without a runtime, and without assuming Claude Code's plugin system.

## 2. Scope

In scope:
- End-to-end software lifecycle guidance for DANMAOB's stack.
- Role definitions an operator can paste into any LLM chat, or wire up
  as subagents in tools that support them (Claude Code, Cursor, etc.).
- Reusable technical and process knowledge (skills) that agents and
  humans both reference.
- Lightweight, staged workflows that describe *who does what, in what
  order, with what handoff* — designed to fit inside a single free-tier
  context window per stage.
- Global engineering rules, a handful of repeatable commands, and
  document templates.

Out of scope for 0.1.0:
- A runtime, CLI, installer, or hook system. DEK is a Markdown
  knowledge/process kit, not executable software.
- Multi-agent orchestration frameworks, daemons, or IDE-specific
  plugin packaging.
- Full parity with ECC's catalog size. DEK covers DANMAOB's actual
  stack and lifecycle needs, not every language/framework ECC supports.

## 3. Principles

1. **Responsibility-first, not technology-first.** Structure follows
   engineering responsibilities (architecture, backend, data,
   frontend, mobile, quality, security, delivery), not a 1-to-1 map of
   technologies to agents/skills.
2. **Context economy by default.** Every file is written to be loaded
   on its own — an agent definition plus the two or three skills and
   rules a task actually needs, not the whole kit.
3. **Provider-agnostic core, provider-aware edges.** Role, skill,
   workflow, and rule content never assumes a specific LLM. A short
   per-provider usage note lives only in `docs/LLM-PROVIDER-GUIDE.md`.
4. **Free-tier first, paid-tier ready.** The default workflow granularity
   assumes one agent, one stage, one bounded context per turn. Nothing
   about the structure prevents running the same agents/skills with
   larger contexts, more parallelism, or automated orchestration later.
5. **Traceable adaptation.** Every non-trivial borrowing from ECC is
   logged in `docs/ECC-TRACEABILITY.md` as KEEP / ADAPT / REMOVE / CREATE
   with a one-line rationale.
6. **Small, coherent team over maximal catalog.** Prefer 11 sharply
   scoped agents over 30 overlapping ones; prefer ~28 focused skills
   over hundreds of thin ones.

## 4. Product / Business Capabilities

Covered by the `product-analyst` agent, the `discovery-and-requirements`
and `planning` workflows, and the `requirements-elicitation`,
`user-stories-acceptance-criteria`, and `estimation-prioritization`
skills:
client/business discovery, problem definition, requirements analysis,
scope definition, backlog preparation, user stories, acceptance
criteria, estimation, prioritization, project planning, and
stakeholder-facing documentation.

## 5. Engineering Capabilities

Architecture and system/API/database design; backend implementation
(C#/.NET/ASP.NET Core/EF Core); database engineering (SQL Server/T-SQL);
frontend implementation (React/TypeScript); mobile implementation
(.NET MAUI); testing (unit, integration, API, frontend, mobile, E2E);
security review; code review; DevOps/CI/CD/deployment; documentation;
maintenance.

## 6. Technology Scope

| Layer      | Technologies |
|------------|--------------|
| Backend    | C#, .NET, ASP.NET Core, REST APIs, Entity Framework Core |
| Database   | Microsoft SQL Server, T-SQL |
| Frontend   | React, TypeScript |
| Mobile     | .NET MAUI, C#, XAML, MVVM |
| Delivery   | Git, GitHub, automated testing, CI/CD, security tooling |

DEK does not mandate one architectural style (Clean, Vertical Slice,
Layered, Modular Monolith) for every project — `architect` and the
`system-architecture-patterns` skill choose per project.

## 7. LLM Strategy

### 7.1 Free-tier strategy (default, 0.1.0)
- One agent persona active per turn; the operator (human or a simple
  script) selects the agent by copying its file (plus 1–3 named
  skills/rules) into the chat, or by pointing a subagent-capable tool
  at the file.
- Workflows are **staged**: each stage names its one active agent, its
  required inputs (small, named artifacts — a spec file, a diff, a
  ticket), and its output artifact. No stage requires the full
  project in context.
- Skills are short (roughly 100–250 lines) and self-contained so a
  single skill plus an agent definition comfortably fits a small
  context window.
- Persistent project artifacts (specs, ADRs, the backlog, test
  reports) are files, not chat history — re-reading a file is cheaper
  than re-deriving its content.
- No workflow requires more than one agent active at a time by default.

### 7.2 Paid/stronger-tier evolution strategy
Nothing in the file structure blocks scaling up:
- Multiple agents can run concurrently (e.g. one LLM session per
  agent) once the operator has the budget/tooling for it; workflow
  files already document the handoff contract between agents, which is
  the only thing true orchestration needs.
- Larger context budgets simply mean loading more skills/rules per
  turn, or letting one agent hold more of a workflow at once.
- Provider-specific automation (hooks, subagents, tool use) can be
  layered on top of these same files without changing their content —
  see `docs/LLM-PROVIDER-GUIDE.md`.

## 8. Agent Architecture

11 agents, defined in `agents/`. Each agent file states: responsibility,
explicit scope (what it does / does not do), expected inputs and
outputs, the skills and rules it draws on, and interaction/handoff
expectations with other agents.

| Agent | Responsibility |
|---|---|
| `product-analyst` | Business/client discovery, requirements, user stories, backlog, estimation, planning |
| `architect` | System architecture, API and database design decisions, technology trade-offs |
| `database-engineer` | SQL Server schema design, T-SQL, indexing, performance, migrations |
| `backend-engineer` | C#/.NET/ASP.NET Core/EF Core implementation |
| `frontend-engineer` | React/TypeScript implementation |
| `mobile-engineer` | .NET MAUI implementation |
| `qa-engineer` | Test strategy and implementation across all layers |
| `security-reviewer` | Security review across the stack |
| `code-reviewer` | Cross-cutting code quality and maintainability review |
| `devops-engineer` | Git/GitHub, CI/CD, deployment, release, environment/maintenance |
| `tech-writer` | Documentation across the lifecycle |

Agents do not overlap in primary responsibility. `code-reviewer` and
`security-reviewer` both look at code but for different concerns
(quality/maintainability vs. exploitable risk) and are meant to run as
separate passes, not merged, because mixing the two dilutes both.

## 9. Skill Architecture

28 skills under `skills/<skill-name>/SKILL.md`, grouped by domain:
product/process (3), architecture & API design (2), database (2),
backend (4), frontend (5), mobile (1), testing (4), security (2),
delivery (4), and one DEK-specific meta-skill
(`free-tier-llm-operating-model`) that explains how to work within
this kit under tight LLM budgets. See `docs/GETTING-STARTED.md` for the
full index. Skills are referenced by name from agent and workflow
files rather than duplicated inline.

## 10. Workflow Architecture

13 staged workflows under `workflows/` (12 in 0.1.0, +1 in 0.1.1),
each naming the responsible agent(s) per stage, inputs, outputs, and
exit criteria: `discovery-and-requirements`, `planning`,
`architecture-design`, `feature-backend` (covers API + database
changes together, since they are usually one unit of work),
`feature-frontend`, `feature-mobile`, `bug-fixing`, `testing`,
`security-review`, `code-review`, `deployment`,
`documentation-and-maintenance`, and (added 0.1.1)
`brownfield-onboarding` — inventorying and documenting an existing,
under-documented system before designing a change against it. See
`docs/ECC-TRACEABILITY.md` for why this was added.

## 11. Rule Architecture

12 rule files under `rules/` (11 in 0.1.0, +1 in 0.1.1): 8
language-agnostic rules in `rules/common/` (architecture, security,
testing, git, error-handling, performance, documentation, and, added
0.1.1, `untrusted-content-and-prompt-safety`) always apply; 4
stack-specific rule files (`rules/csharp-dotnet`,
`rules/typescript-react`, `rules/sql-server`, `rules/dotnet-maui`)
apply only when working in that stack and take precedence over a
common rule where the two genuinely conflict (added 0.1.1 — see each
stack file's "Rule priority" note). Rules are short, enforceable, and
checked for contradictions during validation.

## 12. Command Architecture

7 commands under `commands/` (6 in 0.1.0, +1 in 0.1.1), written as
short, provider-neutral playbooks (not tool-specific slash-command
syntax): `plan-feature`, `review-code`, `security-scan`,
`write-tests`, `update-docs`, `prepare-release`, and (added 0.1.1)
`save-progress` — closing out a session mid-task under free-tier
limits. Each names the agent(s)/skills it invokes and the expected
output. Harnesses that support native slash commands or subagents can
wire these in directly; chat-only usage means pasting the command
file as the turn's instruction.

## 13. Template Architecture

7 templates under `templates/` (6 in 0.1.0, +1 in 0.1.1): user story,
acceptance criteria, ADR (architecture decision record), pull request
description, bug report, API endpoint specification, and (added
0.1.1) a session handoff note pairing with `commands/save-progress.md`.

## 14. Agent Coordination

Coordination is handoff-based, not orchestration-based, in 0.1.0:
a workflow stage ends when its agent produces a named artifact; the
next stage's agent consumes that artifact as its input. No agent
needs another agent's live context — only its output file. This is
what keeps DEK usable one free-tier session at a time, and it is also
exactly the contract a future orchestrator would need, so moving to
paid/automated multi-agent execution later does not require
re-designing the workflows.

## 15. Lifecycle Coverage

Discovery → requirements → planning → architecture → design →
implementation (backend/frontend/mobile/database) → testing →
security → review → delivery/deployment → documentation →
maintenance. Each stage maps to at least one workflow and one agent
(§8, §10).

## 16. Quality Strategy

Quality is enforced through: `code-reviewer` and `security-reviewer`
running as separate, fresh-context passes on any non-trivial change;
`rules/common/*` applying to all work regardless of stack; the
`code-review-checklist` skill; and the `review-code` command as a
repeatable entry point. DEK does not target a numeric coverage
percentage; `qa-engineer` and `rules/common/testing.md` favor
meaningful behavioral verification.

## 17. Testing Strategy

`qa-engineer` plus the `dotnet-testing`, `frontend-testing-and-accessibility`,
`mobile-testing`, and `e2e-testing` skills cover unit, integration, API,
frontend, mobile, and end-to-end testing. TDD (write a failing test,
then implement) is the default approach for backend and frontend
feature work, documented in `workflows/feature-backend.md` and
`workflows/feature-frontend.md`.

## 18. Security Strategy

`security-reviewer` plus `security-checklist-owasp` and
`secure-configuration-secrets` skills cover authentication,
authorization, access control, secret management, input validation,
SQL injection, XSS, CSRF, API security, dependency vulnerabilities,
secure configuration, and secure logging. `rules/common/security.md`
applies these as always-on constraints. DEK never includes credentials,
API keys, tokens, or secrets in any of its own files, and instructs
agents never to introduce them into a project.

## 19. Documentation Strategy

`tech-writer` plus `documentation-standards` skill and the
`documentation-and-maintenance` workflow keep project documentation
(not DEK's own documentation) current. DEK's own documentation
(`README.md`, this spec, `docs/*`) is scoped to what a new user needs
to operate and extend the kit — not generated for volume.

## 20. Git/GitHub Strategy

`devops-engineer` plus `git-workflow` and `cicd-pipelines` skills and
`rules/common/git.md` cover branching, commit conventions, PR process,
and CI/CD pipeline design. DEK itself ships no `.git` metadata and no
CI configuration of its own — it is a knowledge/process kit dropped
into a project's repository, not a repository with its own pipeline.

## 21. ECC Adaptation Strategy

Every ECC-derived idea is classified KEEP / ADAPT / REMOVE / CREATE in
`docs/ECC-TRACEABILITY.md`, based on direct inspection of the
`affaan-m/ECC` repository's public README and file catalog (agents,
skills, commands, rules structure, hooks concept, and TDD/
code-review/security-scan workflow shapes). Concretely (0.1.0
analysis, retained below as-is):

**0.1.1 addendum:** a second, deeper review (individual ECC agent,
skill, rule, and command files, not just the catalog/README) used the
classification KEEP / ADAPT / ADD / REJECT — ADD and REJECT replacing
REMOVE/CREATE's role for this pass, since 0.1.1 was reviewing what to
change in an *existing* DEK rather than deciding a from-scratch
design. Results are appended to `docs/ECC-TRACEABILITY.md` under its
own dated section rather than rewriting the table below.
- **KEEP** (concept only, re-expressed in plain Markdown, no runtime):
  separating rules (always-loaded) from skills (loaded on demand) from
  agents (scoped roles); a plan → implement → review → verify loop;
  fresh-context review as a distinct pass from implementation.
- **ADAPT**: ECC's per-language reviewer/build-resolver agent pattern
  becomes DANMAOB's single `backend-engineer` / `frontend-engineer` /
  `mobile-engineer` / `database-engineer` roles, since DEK targets one
  fixed stack instead of 10+ languages; ECC's TDD workflow becomes
  DEK's `feature-backend`/`feature-frontend` workflows, minus the
  hook-enforced RED/GREEN evidence capture (no runtime in 0.1.0);
  ECC's security-scan concept becomes the `security-review` workflow
  and `security-scan` command, run by an LLM agent instead of a
  static-analysis binary.
- **REMOVE**: hooks/runtime automation, session/memory-vault tooling,
  multi-harness installers, orchestrator daemons, and any
  language/framework coverage outside DANMAOB's stack (Go, Rust, PHP,
  Swift, HarmonyOS, ML pipelines, etc.) — none of it is needed for a
  Markdown-only, single-stack kit.
- **CREATE**: everything DANMAOB-stack-specific (SQL Server/T-SQL,
  ASP.NET Core, .NET MAUI content) and everything free-tier-specific
  (the `free-tier-llm-operating-model` skill, the handoff-based
  coordination model in §14) — ECC does not need these because it
  assumes a paid, hook-capable Claude Code runtime.

## 22. Exclusions

No runtime/hooks, no installer, no orchestrator, no IDE-specific
plugin manifests, no languages/frameworks outside DANMAOB's stack, no
credentials or secrets, no ECC source files or `.git` metadata copied
into DEK.

## 23. Validation Criteria

See `docs/VALIDATION.md` for the full checklist and
`BUILD-REPORT.md` for the results actually obtained for 0.1.0.

## 24. Versioning

Initial release: **DEK 0.1.0**. Version is recorded in `VERSION`,
this spec, and `BUILD-REPORT.md` (0.1.0) / `BUILD-REPORT-0.1.1.md`
(0.1.1 onward, incremental), and should be bumped together on any
future structural change. **0.1.1** (current) added one rule, one
workflow, one command, and one template based on a deeper ECC review
— see `docs/ECC-TRACEABILITY.md`'s 0.1.1 addendum and
`BUILD-REPORT-0.1.1.md`.
