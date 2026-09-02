# Workflow: Brownfield Onboarding (added 0.1.1)

**Agent(s):** `architect` (lead), `product-analyst` (recovering intent
from stakeholders where documentation is missing)
**Skills:** `system-architecture-patterns`, `sql-server-and-tsql`
**Stage input:** Access to an existing, already-running system with
incomplete or absent documentation.
**Stage output:** A system inventory, a recovered/inferred
requirements note, and an architecture-as-understood document —
ready to feed into `discovery-and-requirements`/`architecture-design`
for the actual change being requested.

Why this exists: DANMAOB works on existing client systems at least as
often as new ones, and designing a change against a guessed-at
understanding of an existing system is a common, expensive mistake.
This workflow runs once per system (or after a long gap), not once
per feature.

## Steps
1. **Inventory** — `architect` catalogs what actually exists: major
   modules/services, the database schema as it actually is (not as
   documented, if the two differ), external integrations, deployment
   topology, and anything obviously fragile or undocumented.
2. **Recover intent** — `product-analyst` talks to available
   stakeholders (or reviews existing tickets/support history) to
   recover *why* non-obvious parts of the system work the way they
   do; record this as plainly as possible, including "we don't know
   why" where that's the honest answer.
3. **Document architecture-as-understood** — `architect` writes a
   short document describing the system's actual current architecture
   (not the target state) — enough for `backend-engineer`,
   `frontend-engineer`, `mobile-engineer`, and `database-engineer` to
   orient themselves without re-deriving it from the code every time.
4. Flag anything discovered that looks like a security risk or a data
   integrity risk on its own, independent of the requested change —
   route it to `security-review` even if it's out of scope for the
   current ask.

## Exit criteria
A new team member (human or a fresh LLM session) could read the
inventory and architecture-as-understood document and start
reasoning about a change without re-exploring the whole codebase
first.

## Handoff
→ `discovery-and-requirements` and `architecture-design` for the
actual requested change, now grounded in a real understanding of the
existing system rather than assumptions.
