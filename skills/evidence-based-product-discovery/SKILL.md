---
skill: evidence-based-product-discovery
used_by: [product-analyst]
added_in: incremental ECC extraction (post-0.1.1)
source: ADAPT of ECC's commands/prp-prd.md ("Product Requirements
  Document Generator" — problem-first, hypothesis-driven, hosted at
  https://github.com/affaan-m/ECC/blob/main/commands/prp-prd.md)
---

# Evidence-Based Product Discovery

This skill complements `requirements-elicitation` and
`user-stories-acceptance-criteria` — it does not replace them. Use it
*before or alongside* requirements-elicitation when a request is
large enough, or vague enough, that jumping straight to user stories
risks building the wrong thing. For a small, well-understood ask,
`requirements-elicitation` alone is still enough.

## The core discipline: problem before solution

Work through this order, and don't skip ahead:

```
Problem -> User -> Evidence -> Goal -> Proposed solution
```

Do not let a proposed solution's shape influence how the problem gets
described. If you notice yourself writing the solution first and
back-filling a problem statement to justify it, stop and restate the
problem independently.

## Foundation questions

Before writing anything down, get real answers to:
1. **Who** has this problem? Not "users" — what specific type of
   person or role?
2. **What** problem are they facing? The observable pain, not the
   assumed need.
3. **Why can't they solve it today?** What do they currently do
   instead, and why does it fall short?
4. **Why now?** What changed that makes this worth doing now rather
   than later?
5. **How will you know it's solved?** What would success actually
   look like?

If the person asking can't answer these, that's useful information —
record "unknown, needs research" rather than inventing a plausible
answer.

## Evidence vs. assumption (mandatory tagging)

Every claim in a discovery document gets one of these tags. This is
the single most important discipline in this skill — it's what stops
an LLM's plausible-sounding guess from silently becoming a
requirement.

| Tag | Meaning |
|---|---|
| **Fact** | Directly observed or stated by the client/stakeholder |
| **Evidence** | A data point, quote, ticket volume, or comparable case that supports a claim |
| **Assumption** | Believed true but not confirmed — name what would confirm or refute it |
| **Hypothesis** | A testable belief about what will happen if this is built |
| **Needs validation** | Explicitly unresolved — do not proceed to build on this until it's checked |

**Anti-pattern to actively avoid:** filling a discovery document with
plausible-sounding prose to make it look complete. If information is
missing, write "TBD — needs research" or "Assumption — needs
validation through [specific method]," not an invented specific.

## MVP and anti-goals

- **MVP definition**: the smallest thing that actually tests the
  hypothesis — not the smallest thing that's easy to build.
- **Must / Should / Could / Won't** (reuse DEK's existing MoSCoW
  approach from `estimation-prioritization` — don't introduce a
  second prioritization scheme here).
- **Anti-goals / explicit non-goals**: what this is deliberately NOT
  trying to do, stated as plainly as the goals. Include who is
  explicitly *not* the target user, if relevant — this prevents scope
  creep toward "well, what about this other user too?"
- **Success metrics**: specific and measurable, not "improve the
  experience." If a real number can't be named yet, say so rather
  than inventing a plausible-looking target.

## Validation status

Before treating a discovery document as ready to hand to `architect`,
check its own validation state honestly:

| Section | Status |
|---|---|
| Problem statement | Validated / Assumption |
| Evidence | Present / Needed |
| Technical feasibility | Assessed (with `architect`) / TBD |
| Success metrics | Defined / Needs refinement |

A discovery document with several "Assumption" or "TBD" rows isn't
wrong — it's honest. Flag it clearly rather than smoothing it over,
and name the recommended next step (a stakeholder conversation, a
quick technical spike, a small prototype) rather than proceeding to
full requirements as if everything were settled.

## Output

Use `templates/problem-brief-template.md` to record this. It feeds
`requirements-elicitation` and `user-stories-acceptance-criteria` —
this skill establishes *why* something should be built and what
"solved" looks like; those skills turn it into buildable stories.
