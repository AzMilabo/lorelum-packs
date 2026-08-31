---
id: agentic-coding.planning.define-stop-condition
title: Define Stop and Replanning Conditions
stage: planning
tech_stack:
  - agentic-coding
applies_when: >-
  accepted work is about to begin and the task admits open-ended improvement,
  but there is no explicit execution boundary for completion, deferral, or a
  material signal that must return the work to planning
severity: warn
anti_patterns:
  - id: agentic-coding.planning.opportunity-driven-continuation
    name: Opportunity-driven continuation
    description: >-
      The agent keeps adding adjacent cleanup, abstraction, features, or checks
      after the accepted result is reachable, turning every discovered
      opportunity into current scope and obscuring when the task is done.
    severity: warn
---

## When to apply

Apply immediately before execution when a task could continue indefinitely through nearby improvements or discoveries. The distinguishing need is to set the boundary in advance. If an unplanned public surface, failure mode, or cost increase has already appeared during implementation, pause and replan from the observed drift.

## Guidance

Write one execution boundary that states the observable condition for stopping, which adjacent opportunities are deferred, and which material signals require replanning rather than automatic continuation. Replanning signals should reflect real changes in scope, risk, authority, cost, or evidence feasibility, not ordinary implementation detail. If completion cannot yet be stated, return to the unresolved requirement instead of using “until it looks good.” Stop planning once the boundary lets an observer decide continue, finish, defer, or replan from current facts.

## Anti-pattern

After meeting a narrow export requirement, the agent continues into a generic plugin system because the code reveals a possible extension point. No new authority or risk justifies the continuation, and completion recedes with every opportunity.

## Why

A precommitted boundary prevents implementation momentum and novelty from redefining success. Explicit replanning signals preserve flexibility for material discoveries without treating every idea as either mandatory work or forbidden change.

## Exceptions and boundaries

Incident response, active safety containment, or exploratory research may use timeboxed or evidence-based stopping conditions rather than a fixed deliverable. A newly discovered security, privacy, data-loss, or compatibility risk can require immediate containment before the full replan, but it should still be recorded as a boundary change.

## Example

For adding one supported export format, stop when the accepted format produces the required artifact and planned evidence passes. Defer other formats; replan only if the shared writer must change a public contract or the validation route proves unavailable.
