# Getting Started with DEK

## What you need to know first
- DEK is Markdown, not software. There is nothing to install or run.
- Read `README.md` for the folder layout, then this file for a walked
  example.
- Read `skills/free-tier-llm-operating-model/SKILL.md` before running
  a real project through DEK on a free-tier LLM plan.

## Concepts in one paragraph each

**Agents** (`agents/`) are role definitions: one clear responsibility,
explicit scope, expected inputs/outputs, and the skills/rules they
use. Load one agent per turn.

**Skills** (`skills/<name>/SKILL.md`) are reusable knowledge —
patterns, checklists, decision guides — referenced by name from agent
and workflow files instead of duplicated inline.

**Workflows** (`workflows/`) describe a stage of the lifecycle: which
agent(s), which skills, what input, what output, and what happens
next. A workflow is the unit of "one session's worth of work."

**Rules** (`rules/`) are always-on standards: `common/` applies to
everything, and one stack-specific folder applies depending on what
you're touching (`csharp-dotnet`, `typescript-react`, `sql-server`,
`dotnet-maui`).

**Commands** (`commands/`) are short playbooks that name which
workflow(s) to run for a common request ("review this PR", "run a
security scan").

**Templates** (`templates/`) are fill-in-the-blank documents used by
several workflows.

## Walked example: adding a small feature end-to-end

Say the ask is: "Let clients request a refund from the order page."

1. **Discovery & requirements** — open
   `workflows/discovery-and-requirements.md`, load `product-analyst`
   plus `requirements-elicitation` and
   `user-stories-acceptance-criteria`. Produce a requirements note and
   1–2 user stories with acceptance criteria. Save them as project
   files.
2. **Planning** — open `workflows/planning.md`, load
   `product-analyst` plus `estimation-prioritization`. Size and order
   the stories.
3. **Architecture** — open `workflows/architecture-design.md`, load
   `architect` plus `api-design` and `sql-server-and-tsql`. Decide
   whether this needs a new endpoint and/or schema change; write the
   API contract and, if needed, a database design brief and an ADR.
4. **Backend implementation** — open `workflows/feature-backend.md`,
   load `database-engineer` (if schema changed) then
   `backend-engineer` with `aspnet-core-patterns`, `ef-core-patterns`,
   `dotnet-testing`. TDD the endpoint.
5. **Frontend implementation** — open `workflows/feature-frontend.md`,
   load `frontend-engineer` with `frontend-api-integration` and
   `forms-and-validation`. Build the refund button/flow.
6. **Testing** — open `workflows/testing.md`, load `qa-engineer`.
   Map acceptance criteria to tests across backend and frontend.
7. **Security review** — open `workflows/security-review.md`, load
   `security-reviewer`. Refunds touch money and authorization — this
   stage is not optional here.
8. **Code review** — open `workflows/code-review.md`, load
   `code-reviewer`.
9. **Deployment** — open `workflows/deployment.md`, load
   `devops-engineer`.
10. **Documentation** — open
    `workflows/documentation-and-maintenance.md`, load `tech-writer`.

Each numbered step is a candidate for its own LLM session — none of
them need the others' full chat history, only the file each previous
stage produced.

## Where to go next
- `docs/ECC-TRACEABILITY.md` — what DEK borrowed from ECC and why.
- `docs/LLM-PROVIDER-GUIDE.md` — provider-specific usage notes.
- `docs/EXTENDING-DEK.md` — adding new agents/skills/workflows/rules.
- `docs/VALIDATION.md` — how this release was checked.
