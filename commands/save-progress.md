# Command: save-progress (added 0.1.1)

**Invokes:** whichever agent is currently active
**Use when:** ending a session mid-task, or context is running low,
and the work isn't at a natural stage boundary yet.

## Instruction
Fill out `templates/session-handoff-template.md` with the current
task, what's actually done, the single next step, and any open
question — and save it as a project file. See
`skills/free-tier-llm-operating-model/SKILL.md` for why this matters
under free-tier session limits.

## Output
A saved session handoff note that the next session (same or different
LLM) can load instead of needing the prior chat history.
