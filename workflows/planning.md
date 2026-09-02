# Workflow: Planning

**Agent(s):** `product-analyst`
**Skills:** `estimation-prioritization`
**Stage input:** Stories/backlog from `discovery-and-requirements`.
**Stage output:** A prioritized, estimated backlog slice ready for
architecture/design.

## Steps
1. Size each story (relative sizing, not false-precision hours).
2. Prioritize using value/effort or MoSCoW.
3. Flag any story whose estimate depends on an architectural unknown —
   route that story to `architecture-design` before committing to a
   plan.
4. **Break large stories into small, independently shippable
   increments** (added 0.1.1): if a story can't reasonably be
   implemented, reviewed, and deployed as one unit, split it so each
   piece can be reviewed and, if needed, rolled back on its own rather
   than as part of one large, hard-to-revert change.

## Exit criteria
The next slice of work is ordered and each item has a size.

## Handoff
→ `architecture-design` (for anything needing a technical decision) or
directly to the relevant `feature-*` workflow if the design is already
obvious/small.
