---
id: agentic-coding.implementation.replan-on-material-drift
title: Replan When Implementation Materially Drifts
stage: implementation
tech_stack:
  - agentic-coding
applies_when: >-
  implementation has revealed an unplanned public surface, source type,
  fallback, I/O pass, file group, risk class, or evidence need, and the agent
  is about to continue coding as though the accepted plan still applies
severity: warn
anti_patterns:
  - id: agentic-coding.implementation.drift-normalization
    name: Drift normalization
    description: Absorbing each unplanned expansion as a small local edit until the implementation has a different scope, risk, or proof burden than the accepted plan.
    severity: warn
---

## When to apply

Apply when implementation discoveries materially change what will be delivered, who may depend on it, how it can fail, or what evidence is needed. A routine file move, renamed helper, or local adjustment already covered by the accepted scope and risk is a near miss. The trigger is changed planning truth, not ordinary implementation detail.

## Guidance

Pause the expanding work and compare the discovery with the accepted scope, risk level, stop condition, and evidence plan. Produce one revised implementation baseline: either narrow back to the plan, explicitly admit the new work with updated risk and evidence, or stop for authorization. Resume only from that decision. Do not keep coding while treating the update as documentation to be completed later.

## Anti-pattern

Allowing a helper to become a public protocol, then adding a fallback, another input type, and a second I/O pass one at a time because no individual edit appears large enough to justify replanning.

## Why

Plans calibrate scope and verification against known risk. Material drift invalidates that calibration; continuing silently compounds commitments and leaves testing and review aimed at an obsolete target. Replanning early makes the changed cost and proof burden visible before they are entrenched.

## Exceptions and boundaries

Urgent containment of an active security or data-loss incident may precede formal replanning, but the response should still minimize exposure and record the changed baseline as soon as safe. Do not invoke this Practice for harmless mechanical details, and do not use it to reopen settled scope without material new evidence.

## Example

A private import adapter begins requiring a new public source type and network fallback. The agent pauses, rejects the fallback as outside scope, and updates the plan to cover only the adapter plus its revised validation evidence before resuming.
