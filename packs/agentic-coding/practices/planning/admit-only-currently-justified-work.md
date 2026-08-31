---
id: agentic-coding.planning.admit-only-currently-justified-work
title: Admit Only Currently Justified Work
stage: planning
tech_stack:
  - agentic-coding
applies_when: >-
  candidate plan items are being reviewed before commitment, and one or more
  items may be promoted to required work based only on generic practice,
  possible future use, or visible output
severity: warn
anti_patterns:
  - id: agentic-coding.planning.future-value-scope-promotion
    name: Future-value scope promotion
    description: >-
      The agent promotes an abstraction, fallback, feature, or guardrail into
      required work because it might be useful later, expanding current cost and
      maintenance without a present requirement or evidenced risk.
    severity: warn
---

## When to apply

Apply while deciding which proposed items belong in the committed plan. The trigger is a plausible item whose current basis is uncertain, not a public-surface change already being implemented. This Practice reviews all candidate work; it does not perform the later design check for a particular interface or extension point.

## Guidance

Give each candidate item one scope disposition: required, optional, or out of scope. Mark it required only when it directly supports a current acceptance condition, evidenced risk, stable contract, or explicitly approved expansion. A useful idea without that basis remains optional and must not become an implementation dependency. If its status depends on a missing authority decision, leave it unresolved and request that decision rather than upgrading it by default. Stop when every committed item has a present, traceable reason.

## Anti-pattern

A plan for one supported data source adds arbitrary file and network locators “for flexibility.” The extra locators become required work even though no current user, contract, or risk calls for them.

## Why

Scope expands most cheaply in a plan and most expensively after code, tests, and compatibility expectations attach to it. Requiring present justification blocks proxy achievements such as more features or more abstractions from displacing the requested result.

## Exceptions and boundaries

Security, privacy, data integrity, compatibility, and compliance protections may be required by an evidenced risk or governing contract even when they are not named in the feature request. Conversely, this Practice does not forbid recording optional improvements; it prevents them from silently becoming commitments.

## Example

For a task that explicitly requires one custom registry, admit the narrow registry path as required. Record support for arbitrary locators as optional because “it may be useful someday” is not current justification.
