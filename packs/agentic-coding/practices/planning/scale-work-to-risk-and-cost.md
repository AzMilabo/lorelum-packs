---
id: agentic-coding.planning.scale-work-to-risk-and-cost
title: Scale Work to Risk and Cost
stage: planning
tech_stack:
  - agentic-coding
applies_when: >-
  an implementation approach is being chosen for the first time, and the agent
  is about to set reasoning, testing, review, and rollback depth for work whose
  blast radius, reversibility, uncertainty, or failure cost materially varies
severity: warn
anti_patterns:
  - id: agentic-coding.planning.uniform-engineering-ceremony
    name: Uniform engineering ceremony
    description: >-
      The agent applies the same heavy or light engineering template to every
      task, wasting effort on reversible changes or omitting necessary protection
      from changes with costly failure modes.
    severity: warn
---

## When to apply

Apply before implementation when choosing how much engineering investment the task warrants. The distinguishing condition is that failure exposure, reversibility, uncertainty, or recovery cost must set the initial depth. If implementation has already revealed a material new risk or scope change, replan from that discovery instead of merely defending the original estimate.

## Guidance

Assess the credible blast radius, reversibility, uncertainty, and cost of failure, including harm to users, data, security, compatibility, and operations. Choose one proportional investment level and state what it implies for analysis, verification, independent review, and recovery preparation. Increase depth only for a concrete exposure or mandatory policy; decrease it when the change is local, observable, and cheaply reversible. If a material factor is unknown, resolve it or plan a bounded probe before fixing the level. Stop when the planned safeguards can be explained by the task's actual failure profile.

## Anti-pattern

A text-only styling correction receives a migration plan, broad regression suite, and rollback mechanism because those artifacts signal thoroughness. Meanwhile, applying the same template lightly to an authorization change would miss denied-path and recovery evidence.

## Why

Proportional investment directs attention toward failure modes that matter instead of toward a familiar artifact count. It reduces waste on low-risk work without turning simplicity into a reason to under-protect high-impact changes.

## Exceptions and boundaries

An organizational policy may mandate a review or check regardless of local risk; treat that policy as part of the cost model rather than bypassing it. Unknown security, privacy, or data-loss exposure should bias toward more investigation until bounded, not toward a smaller plan for convenience.

## Example

For a reversible copy edit, choose a focused visual check. For a permission-rule change, choose denied-path tests, integration evidence, independent review, and a recovery route because the failure can expose protected actions.
