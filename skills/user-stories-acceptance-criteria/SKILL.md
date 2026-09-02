---
skill: user-stories-acceptance-criteria
used_by: [product-analyst]
templates: [user-story-template, acceptance-criteria-template]
---

# User Stories & Acceptance Criteria

## Format
`As a <role>, I want <capability>, so that <benefit>.`
Keep the benefit honest — if you can't state why it matters, the story
may not be ready to build yet.

## Sizing
A story should be completable and testable in isolation. If a story
needs "and" to describe its capability, it is probably two stories.

## Acceptance criteria
Write criteria as concrete, testable statements — Given/When/Then
works well:
```
Given <context>
When <action>
Then <observable outcome>
```
Include at least one happy path and one edge/failure case per story.
Acceptance criteria are what `qa-engineer` turns directly into test
cases, so vague criteria ("works correctly") are not acceptable.

## Anti-patterns
- Acceptance criteria that describe implementation instead of
  observable behavior.
- Stories with no failure-path criteria at all.
- A backlog of stories with no priority or estimate attached.
