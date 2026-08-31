---
id: agentic-coding.implementation.choose-smallest-sufficient-design
title: Choose the Smallest Sufficient Design
stage: implementation
tech_stack:
  - agentic-coding
applies_when: >-
  two or more feasible implementation designs satisfy the accepted behavior,
  and the agent is about to choose how much abstraction, indirection, state,
  or I/O to introduce while preserving current invariants
severity: warn
anti_patterns:
  - id: agentic-coding.implementation.architecture-for-possibility
    name: Architecture for possibility
    description: Selecting extra layers, branches, or passes for imagined future uses when a smaller design already satisfies current acceptance and invariants.
    severity: warn
---

## When to apply

Apply after feasible options are known and before committing to their structural complexity. The trigger is a design choice among sufficient alternatives, not the earlier question of whether an existing capability can be reused. If only one option satisfies the contract or safety constraints, there is no smallest-sufficient comparison to make.

## Guidance

State the acceptance behavior and invariants every candidate must preserve. Among the candidates that meet them, choose the design with the fewest new responsibilities and the most reversible commitment while fitting existing boundaries. Name the present evidence that would justify any additional layer, state transition, fallback, or I/O pass. The output is one selected design and its sufficiency rationale; stop once added structure no longer protects a current invariant.

## Anti-pattern

Adding a wrapper hierarchy, configurable strategy, extra error taxonomy, and second data pass because each might help a future variant that is neither required nor evidenced.

## Why

Every additional responsibility creates interactions, failure modes, and maintenance commitments. Selecting the least structure that still protects current invariants reduces those costs without confusing “small” with incomplete.

## Exceptions and boundaries

Security isolation, migration safety, published compatibility, measured performance constraints, or an approved near-term requirement can make a larger design the smallest one that is actually sufficient. Do not remove protections just to minimize a diff. A design that violates an existing ownership boundary is not sufficient even if it uses less code.

## Example

Two designs can normalize one input format: a local adapter or a configurable conversion pipeline. With one confirmed format and no extension contract, the agent chooses the adapter and records that the pipeline would require a second supported format.
