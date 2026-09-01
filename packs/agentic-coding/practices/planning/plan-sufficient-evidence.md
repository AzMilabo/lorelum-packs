---
anti_patterns:
  - description: The agent maximizes the number or breadth of convenient checks because they create visible confidence, while none observes the boundary where the required behavior can actually fail.
    id: agentic-coding.planning.check-volume-evidence-plan
    name: Check-volume evidence plan
    severity: warn
applies_when: acceptance conditions are known and implementation is about to begin, but the agent has not chosen observations that can distinguish success from plausible failure at an appropriate cost
id: agentic-coding.planning.plan-sufficient-evidence
severity: warn
stage: planning
tech_stack:
  - agentic-coding
title: Plan the Minimum Sufficient Evidence
---

## When to apply

Apply after acceptance is clear and the task's overall engineering depth has been chosen, but before
coding. Decide how each must will be demonstrated and where cheap evidence stops being
representative. If checks have already run and their coverage is being reconciled with acceptance,
map the evidence instead.

## Guidance

For each must, choose the lowest-cost observation that distinguishes success from a plausible
failure. State its scope, blind spot, and trigger for stronger evidence. Use focused checks to
reject bad approaches early; reserve integration, a representative environment, or human review for
boundaries cheaper checks cannot represent. If no feasible evidence supports a must, expose that
limit before implementation. Stop when every must has a sufficient route or an explicit gap.

## Anti-pattern

An export plan lists unit tests, static checks, and manual file inspection. They are convenient and
all can pass, but none opens the archive in the independent consumer named by the compatibility
requirement. Check volume substitutes for evidence at the only boundary that matters.

## Why

Evidence tied to a plausible failure shows what a pass rules out. The cheapest sufficient route
avoids ceremony while preserving stronger checks where they can change the decision.

## Exceptions and boundaries

Audits, certification, safety cases, or release policy may require more evidence. Exploratory
evidence cannot support a production claim or a claim that the complete feature works.

## Example

A payment retry must not create a duplicate charge. The plan uses focused state-transition tests for
retry rules and one integration observation against a test payment endpoint for idempotency. It
escalates to a controlled staging check only if the real gateway's retry behavior differs from the
test endpoint.
