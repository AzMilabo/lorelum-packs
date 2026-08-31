---
id: agentic-coding.verification.close-or-declare-evidence-gaps
title: Close or Declare Evidence Gaps
stage: verification
tech_stack:
  - agentic-coding
applies_when: an acceptance-to-evidence comparison has exposed a gap, and the agent is about to proceed toward delivery despite evidence that is narrower than the intended outcome
severity: warn
anti_patterns:
  - id: agentic-coding.verification.gap-by-implication
    name: Gap by implication
    description: Inferring an uncovered outcome from a nearby successful check hides the gap and allows the eventual claim to exceed what was observed.
    severity: warn
---

## When to apply

Apply once a concrete mismatch exists between the outcome intended for delivery and the evidence actually available. Do not apply when the task is still selecting its initial verification approach and no gap has yet been observed.

## Guidance

For each material gap, choose one disposition: obtain the missing evidence, narrow the supported outcome to the evidence already available, or mark the outcome incomplete. Base the choice on the consequence of being wrong and the cost or feasibility of the missing check. Stop when every material gap has an explicit disposition; do not manufacture a pass from adjacent evidence.

## Anti-pattern

Assuming that a successful click interaction also proves persisted state after reload, then allowing the untested persistence behavior to disappear inside a general "works" conclusion.

## Why

Unresolved gaps otherwise migrate into delivery language as hidden assumptions. An explicit disposition converts uncertainty into either new evidence, a smaller claim, or visible unfinished work before someone relies on it.

## Exceptions and boundaries

Low-impact gaps may be declared rather than closed when the recipient can make an informed decision with that limitation. Safety, authorization, data integrity, migration, or irreversible-release boundaries may forbid narrowing or deferral and require the missing evidence before proceeding.

## Example

The current check proves a preference changes on screen but cannot verify reload persistence. The agent records the supported outcome as limited to the in-session update.
