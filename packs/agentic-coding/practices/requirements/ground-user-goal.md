---
id: agentic-coding.requirements.ground-user-goal
title: Ground Work in the User Goal
stage: requirements
tech_stack:
  - agentic-coding
applies_when: >-
  a task has just been received or the work is drifting, and the agent is about
  to frame what to build without a current statement of the user-visible outcome
severity: warn
anti_patterns:
  - id: agentic-coding.requirements.solution-shaped-goal
    name: Solution-shaped goal
    description: >-
      The agent restates its preferred implementation or a visible work product
      as the goal, making a technically complete solution able to miss the result
      the user actually needs.
    severity: warn
---

## When to apply

Apply when beginning a task, or when implementation details have started to replace the reason for the work. The trigger is a missing or stale statement of who needs what observable result. If the result is already clear and the only open question is how completion will be judged, define acceptance boundaries instead.

## Guidance

Read the user's current request and any explicitly adopted task source. Produce one concise goal statement naming the affected user or operator, the observable result they need, and any explicit constraint that changes that result. Treat proposed components, abstractions, tests, and documents as means rather than goals. If a material ambiguity permits different user outcomes, mark that ambiguity or ask for a decision; do not resolve it by choosing an implementation. Stop once the outcome statement is specific enough to reject work that would not advance it.

## Anti-pattern

Turning “let administrators manage all roles for one account” into “build a role-assignment table” makes a convenient interface shape the target. The table can work while the user still cannot manage the account as required.

## Why

A stable outcome statement gives later scope and design decisions a common reference. It prevents implementation momentum and easy-to-measure artifacts from silently replacing user value.

## Exceptions and boundaries

For a purely mechanical request whose outcome is already exact, such as renaming a supplied label, the user's wording may already be the complete goal statement. Do not add a planning ceremony. This Practice identifies the desired outcome; it does not enumerate acceptance tests or non-goals.

## Example

Before planning a settings change, record: “Existing users can update their display name and time zone through the current settings flow, without introducing new product behavior.” A proposed marketing description can then be excluded because it does not advance that outcome.
