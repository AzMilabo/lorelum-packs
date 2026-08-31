---
id: agentic-coding.implementation.surface-unconfirmed-assumptions
title: Surface Safe Unconfirmed Assumptions
stage: implementation
tech_stack:
  - agentic-coding
applies_when: >-
  implementation lacks evidence for one interpretation, but work can proceed
  safely and reversibly, and the agent is about to choose a provisional value,
  behavior, or boundary rather than block on confirmation
severity: warn
anti_patterns:
  - id: agentic-coding.implementation.silent-assumption
    name: Silent assumption
    description: Treating an unverified interpretation as established fact, which hides its affected scope and lets later work build on a premise no authority confirmed.
    severity: warn
---

## When to apply

Apply when a specific uncertainty remains, its provisional interpretation has limited and reversible impact, and implementation can safely continue. The near miss is an unknown that would alter a public contract, product behavior, security boundary, irreversible migration, or other high-cost decision; that uncertainty requires confirmation before implementation, not merely disclosure.

## Guidance

Create one explicit assumption record containing the provisional interpretation, the evidence currently supporting it, the affected implementation boundary, and the condition that will confirm or invalidate it. Keep the implementation within that boundary and avoid deriving additional requirements from the assumption. The output is the visible assumption and its review trigger; stop once later work can identify and replace it without reconstructing the exploration.

## Anti-pattern

Choosing a plausible default, coding several dependent behaviors around it, and describing the result as required behavior even though the source material never settled that choice.

## Why

An unspoken assumption is easily promoted to fact by later code, tests, summaries, or handoffs. Making it explicit preserves uncertainty and limits propagation while still allowing low-risk progress.

## Exceptions and boundaries

Do not use an assumption record to bypass conflicting authoritative sources or a decision that needs product, security, legal, or operational approval. Purely local implementation details that are fully determined by existing conventions do not need ceremony. If new evidence invalidates the assumption, revise the affected work rather than preserving the assumption as compatibility behavior.

## Example

An API example omits whether timestamps include fractional seconds, while all current responses use whole seconds and parsing is tolerant. The agent records “emit whole seconds pending contract confirmation,” limits the choice to serialization, and names contract clarification as the review trigger.
