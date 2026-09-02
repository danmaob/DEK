# Extending DEK

## Adding a new skill
1. Create `skills/<kebab-case-name>/SKILL.md`.
2. Include a small frontmatter block: `skill:`, `used_by:` (which
   agents reference it).
3. Keep it short (roughly 100–250 lines) and self-contained — it
   should make sense loaded alongside one agent file, without the
   rest of DEK.
4. Reference it by name from any agent/workflow file that should use
   it; do not duplicate its content elsewhere.

## Adding a new agent
1. Create `agents/<kebab-case-name>.md` with frontmatter: `agent:`,
   `role:`, `stage:`, `skills:`, `rules:`.
2. Write explicit **Scope** ("Does" / "Does not") — the most common
   failure mode when adding agents is overlap with an existing one.
   Check `DEK-SPEC.md` §8 first.
3. State **Inputs**, **Outputs**, and **Handoff** so the agent slots
   into a workflow's stage structure.
4. Update `DEK-SPEC.md` §8 (agent table) and, if it changes lifecycle
   coverage, §15.

## Adding a new workflow
1. Create `workflows/<kebab-case-name>.md` naming: agent(s), skills,
   stage input, stage output, numbered steps, exit criteria, and
   handoff to the next workflow(s).
2. Keep each workflow scoped to what fits in one free-tier session —
   if it needs more than ~3 skills or 2 agents active at once, split
   it into two workflows with a handoff between them.
3. Update `DEK-SPEC.md` §10.

## Adding a new rule
1. Decide: does it apply regardless of stack (`rules/common/`) or only
   to one stack layer (`rules/<stack>/coding-standards.md`)?
2. Keep rules short and enforceable — a reviewer should be able to
   check compliance from the diff alone, without needing to ask the
   author to explain intent.
3. Check for contradictions with existing rules before adding (see
   `docs/VALIDATION.md`).
4. Update `DEK-SPEC.md` §11.

## Adding a new command or template
- Commands (`commands/`) are one-paragraph pointers to a workflow (or
  a short sequence of workflows) — do not put process detail in a
  command file that belongs in a workflow file.
- Templates (`templates/`) are fill-in-the-blank documents; add one
  when the same document shape is being reproduced ad hoc by more
  than one workflow.

## Versioning a change
Bump `VERSION` and the version line in `DEK-SPEC.md` and `README.md`
together for any change that adds/removes/renames an agent, skill,
workflow, or rule file. Small wording fixes within an existing file do
not require a version bump.
