---
id: agentic-coding.planning.plan-sufficient-evidence
title: Plan the Minimum Sufficient Evidence
stage: planning
tech_stack:
  - agentic-coding
applies_when: >-
  observable acceptance conditions are known and implementation is about to
  begin, but the agent has not selected evidence that can prove each condition
  at appropriate cost or expose a known verification boundary
severity: warn
anti_patterns:
  - id: agentic-coding.planning.check-volume-evidence-plan
    name: Check-volume evidence plan
    description: >-
      The agent maximizes the number or breadth of checks without asking what
      each one proves, increasing cost while still allowing important acceptance
      conditions to remain unsupported.
    severity: warn
---

## When to apply

Apply after acceptance conditions are available and before coding makes validation an afterthought. The trigger is an imminent choice of how the result will be demonstrated, not a later reconciliation of evidence already collected. The planned evidence must be sufficient for the acceptance risk without becoming a generic test inventory.

## Guidance

For each acceptance condition, choose the lowest-cost observation that can actually distinguish success from a plausible failure. State the evidence's scope, any known blind spot, and the condition that would escalate validation to a more expensive level. Prefer focused checks early when they can eliminate bad approaches, while reserving integration, real-environment, or human evidence for boundaries that cheaper checks cannot represent. If no feasible evidence can support a condition, expose that limitation before implementation. Stop when every must has a sufficient evidence route or an explicit verification boundary.

## Anti-pattern

A plan lists unit tests, static checks, and a manual click-through, but none can show that saved data survives reload. The volume of checks creates confidence without covering the persistence condition.

## Why

Designing evidence against specific acceptance conditions prevents easy checks from becoming substitutes for proof. Selecting the cheapest sufficient route also preserves time for boundaries where stronger evidence changes the decision.

## Exceptions and boundaries

Mandatory audits, certification, safety cases, or release gates may require evidence beyond the local minimum; include them as governing constraints. Exploratory work may use provisional evidence, but it must not support a production or full-capability claim.

## Example

For a saved preference, plan a focused behavior check for validation and an integration observation after reload for durability. Escalate to a real environment only if the storage boundary differs materially from the test environment.
