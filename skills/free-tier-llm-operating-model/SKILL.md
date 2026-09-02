---
skill: free-tier-llm-operating-model
used_by: [all agents; read this first when operating under tight LLM limits]
---

# Operating DEK Under Free-Tier LLM Limits

This is DEK's own meta-skill: how to actually run this kit when the
active LLM session has limited requests, limited context, or limited
execution time.

## Per-turn discipline
- Load exactly one agent definition, plus the 1–3 skills and rules it
  names for the current task — not the whole `DEK/` tree.
- Treat each workflow stage (see `workflows/`) as one session's worth
  of work with one clear output artifact; don't try to complete an
  entire multi-stage workflow in one sitting.
- Persist decisions as files (ADRs, specs, backlog entries), not as
  something only remembered in chat history that a new session won't
  see.

## When context runs low mid-task
Write down the current state (what's done, what's next, any open
question) into the relevant artifact file before the session ends,
so the next session — possibly a different LLM entirely — can resume
from the file instead of from chat history. Use
`templates/session-handoff-template.md` and `commands/save-progress.md`
for this.

## Verify against current documentation (added 0.1.1)
Any LLM's knowledge of a framework, library, or API has a cutoff and
can be wrong about recent versions or less-common behavior. When a
task depends on specifics that are easy to get subtly wrong (an
API signature, a config option's default, a library's current
behavior), say so explicitly and check it against current official
documentation rather than asserting it from memory — especially for
fast-moving parts of the stack. This costs one lookup; a wrong
assumption baked into shipped code costs more.

## Choosing what to load
Prefer the smallest set of skills that covers the task. If a task
seems to need four or five skills at once, it is probably actually
two separate workflow stages — split it.

## Scaling up later
None of this changes when DANMAOB moves to a paid/stronger plan —
larger context just means comfortably loading more of the kit at
once, and true multi-agent orchestration can be layered on top of the
same handoff contracts described in each workflow file (see
DEK-SPEC.md §7.2 and §14).
