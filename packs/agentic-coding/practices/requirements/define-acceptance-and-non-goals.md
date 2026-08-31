---
id: agentic-coding.requirements.define-acceptance-and-non-goals
title: Define Acceptance and Explicit Non-goals
stage: requirements
tech_stack:
  - agentic-coding
applies_when: >-
  the user outcome and requirement authority are known, and the agent is about
  to plan or verify work without observable completion conditions and a boundary
  against plausible scope expansion
severity: warn
anti_patterns:
  - id: agentic-coding.requirements.artifact-count-acceptance
    name: Artifact-count acceptance
    description: >-
      The agent defines completion by files, tasks, tests, or documents produced
      rather than observable behavior, allowing busy output to pass while the
      capability remains incomplete or expanded.
    severity: warn
---

## When to apply

Apply after the intended user result is understood but before a plan or verification claim depends on an implicit definition of done. The distinguishing condition is that plausible adjacent work could be mistaken for required scope. If the user outcome itself is still unclear, establish that outcome first rather than inventing acceptance criteria.

## Guidance

Create one compact acceptance boundary in the project's existing task authority. State the smallest set of observable musts that together demonstrate the requested result, then name the most plausible non-goal that would otherwise expand the work. Prefer user behavior, stable contracts, and durable invariants over internal steps or artifact counts. Mark any must that cannot yet be made observable as unresolved rather than weakening it into an implementation proxy. Stop when the boundary can distinguish complete, incomplete, and out-of-scope work.

## Anti-pattern

“Component added, tests written, and documentation updated” can all be true while saved data disappears after refresh. Those outputs do not define the requested behavior and may reward unnecessary additions.

## Why

Observable musts keep planning and evidence tied to the requested capability. An explicit non-goal prevents common optional improvements from quietly becoming promises and then gaining tests, compatibility obligations, and maintenance cost.

## Exceptions and boundaries

For a tiny, fully specified, reversible edit, one observable must and one short boundary may be sufficient; do not manufacture a formal checklist. Security, privacy, authorization, migration, and compatibility constraints remain valid musts even when they require more work than the happy path.

## Example

For a profile edit, define the must as “the new display name remains after save and reload” and the non-goal as “add a new success animation.” A rendered form alone is then visibly incomplete, while animation work is visibly outside the task.
