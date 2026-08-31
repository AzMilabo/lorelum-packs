---
id: agentic-coding.implementation.preserve-responsibility-boundaries
title: Place Behavior With Its Invariant Owner
stage: implementation
tech_stack:
  - agentic-coding
applies_when: >-
  a change crosses domain, layer, package, service, or repository boundaries,
  and the agent is about to decide which component should own behavior that
  enforces a specific invariant
severity: warn
anti_patterns:
  - id: agentic-coding.implementation.invariant-in-wrong-owner
    name: Invariant in the wrong owner
    description: Placing behavior in the nearest editable component instead of the component responsible for its invariant, which duplicates policy and allows callers to diverge.
    severity: warn
---

## When to apply

Apply when a requested behavior touches more than one responsibility boundary and its placement is still undecided. The near miss is a local implementation detail entirely inside the component that already owns the relevant invariant. This Practice decides ownership, not whether the architecture itself should be redesigned.

## Guidance

Name the invariant the behavior must preserve, identify the component already accountable for that invariant, and place the authoritative decision there. Let other layers translate inputs, outputs, or presentation without reimplementing the rule. The output is one ownership placement with a clear boundary for callers. If no existing component legitimately owns the invariant, stop and seek an explicit design decision rather than assigning it by convenience.

## Anti-pattern

Implementing authorization, identity grouping, validation, or consistency rules in a presentation or transport layer because that is where the immediate symptom appears, leaving other callers free to behave differently.

## Why

An invariant enforced by its owner has one semantic source and can be applied consistently across entry points. Putting it in a convenient caller couples policy to one flow and invites duplicated or contradictory behavior elsewhere.

## Exceptions and boundaries

Defense-in-depth checks may repeat validation at a trust boundary, but they should reinforce rather than redefine the authoritative invariant. Performance-sensitive duplication requires evidence and a consistency strategy. If the requirement intentionally changes ownership or splits a domain, handle that as an architectural decision with migration implications.

## Example

A screen needs to show one account with several roles. The agent keeps identity aggregation in the domain service that owns account semantics and lets the screen render the resulting model, rather than teaching the screen to merge authorization rows.
