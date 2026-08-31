---
id: agentic-coding.testing.anchor-tests-to-requirements
title: Anchor Each Test to a Contract
stage: testing
tech_stack:
  - agentic-coding
applies_when: >-
  test coverage is being selected for new or changed behavior, and the agent
  is about to add or modify a test without identifying the requirement,
  stable contract, or domain invariant that the test should protect
severity: warn
anti_patterns:
  - id: agentic-coding.testing.test-without-protected-contract
    name: Test without a protected contract
    description: Adding coverage because code or a screen changed, without naming the behavior that must remain true, which lets tests legitimize an incorrect implementation.
    severity: warn
---

## When to apply

Apply while deciding what a new or changed test is for. The distinguishing decision is the behavior or invariant the test protects. Choosing the exact observation or assertion comes later and is a near miss for this Practice. Mechanical test cleanup that preserves an already explicit contract does not require a new mapping.

## Guidance

For the proposed test, identify one authoritative requirement, published contract, or domain invariant whose violation would matter. Express the protected behavior independently of the current implementation, then admit the test only if its pass/fail result meaningfully represents that behavior. The output is one explicit test-to-contract mapping. If no durable basis can be found, revise the test purpose or omit it rather than treating changed code as sufficient justification.

## Anti-pattern

Mirroring every new component, method, branch, or state with a test even though those structures may encode an incomplete or mistaken interpretation of the user capability.

## Why

Tests become durable evidence and future change constraints. Anchoring each one to a requirement or invariant keeps the suite aligned with intended behavior instead of allowing the current implementation to define correctness by itself.

## Exceptions and boundaries

Exploratory probes and temporary characterization tests can help reveal unknown behavior without yet asserting that it is correct; label and retire or promote them deliberately. Safety, compatibility, and data-integrity invariants may justify tests even when they are not visible in a feature description. This Practice does not prescribe the assertion mechanism.

## Example

Rather than testing that each authorization record renders as one row, the agent maps the test to “an account’s complete role set can be managed together.” That mapping exposes that a row-per-record test would protect the wrong domain behavior.
