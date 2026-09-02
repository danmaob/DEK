# DEK — DANMAOB Engineering Kit

**Version 0.1.1**

DEK is DANMAOB's own AI Software Engineering Team: a set of role
definitions (agents), reusable knowledge (skills), staged processes
(workflows), always-on standards (rules), short repeatable operations
(commands), and document templates — all in plain Markdown, usable
with any capable LLM (Claude, ChatGPT/Codex, Gemini, Qwen, and
others), starting on free-tier plans.

It is specialized for DANMAOB's stack: **SQL Server + C#/.NET/
ASP.NET Core + Entity Framework Core + React/TypeScript + .NET MAUI**,
supported by Git/GitHub, testing, security, and CI/CD.

DEK is derived from ideas in the "Everything Claude Code" (ECC)
open-source project (`github.com/affaan-m/ECC`) but is an independent,
LLM-agnostic, single-stack kit — not a smaller copy of ECC. See
`docs/ECC-TRACEABILITY.md` for exactly what was kept, adapted, removed,
or created.

## Why DEK exists

DANMAOB builds real software projects across the full lifecycle —
discovery, requirements, architecture, implementation, testing,
security, review, deployment, documentation, maintenance — and
currently does this without a paid LLM plan. DEK packages engineering
practice as Markdown so any free-tier chat session can act as a
specific, well-scoped engineering role instead of a generic assistant
re-deriving process from scratch every time.

## How it's organized

```
DEK/
|-- DEK-SPEC.md      # Source of truth for DEK's own architecture
|-- README.md         # This file
|-- VERSION            # Current DEK version
|-- agents/            # 11 role definitions
|-- skills/            # 28 reusable knowledge modules (skills/<name>/SKILL.md)
|-- workflows/         # 13 staged processes tying agents+skills together
|-- rules/             # Always-on standards: common/ (8 files) + 4 stack-specific dirs
|-- commands/          # 7 short, repeatable operations
|-- templates/         # 7 reusable document templates
|-- docs/              # Getting-started, traceability, provider, and extension guides
```

## How to use DEK (chat-only / free-tier)

1. Identify which stage of work you're doing (see `workflows/`).
2. Open the workflow file for that stage — it names the responsible
   agent(s) and the skills/rules it needs.
3. Paste the relevant `agents/<agent>.md` file into your LLM chat as
   the system/role instruction, followed by the 1–3 skill files the
   workflow names.
4. Give the LLM the actual task input (the requirements note, the
   diff, the bug report, etc.) named as that stage's input.
5. Save the stage's output as a project file (spec, ADR, code, test
   plan) so the next stage — possibly a different LLM session
   entirely — can pick it up without needing the chat history.

See `skills/free-tier-llm-operating-model/SKILL.md` for the full
operating discipline, and `docs/GETTING-STARTED.md` for a walked
example.

## How to use DEK with an agentic/subagent-capable tool

If your tool supports subagents or custom instructions (e.g. Claude
Code, Cursor), point it at `agents/<name>.md` as that agent's
definition and `skills/<name>/SKILL.md` files as its available
skills. The files need no reformatting — they are plain Markdown with
a small YAML frontmatter block naming the agent's skills/rules.

## Using DEK with different LLMs

See `docs/LLM-PROVIDER-GUIDE.md` for short, provider-specific notes.
Nothing in `agents/`, `skills/`, `workflows/`, `rules/`, `commands/`,
or `templates/` assumes a specific provider.

## Operating under free-tier limits

See `skills/free-tier-llm-operating-model/SKILL.md` and
`docs/GETTING-STARTED.md`. In short: one agent, one workflow stage,
one bounded context per turn; persist state as files, not chat history.

## Extending DEK

See `docs/EXTENDING-DEK.md` for how to add a new agent, skill,
workflow, or rule without breaking the existing structure.

## Validation

See `docs/VALIDATION.md` for the checklist used to validate this
release, and `BUILD-REPORT.md` for the actual results.
