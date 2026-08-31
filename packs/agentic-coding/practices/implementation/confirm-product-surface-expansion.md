---
id: agentic-coding.implementation.confirm-product-surface-expansion
title: Confirm Authorized Product Surface Variants
stage: implementation
tech_stack:
  - agentic-coding
applies_when: >-
  accepted scope authorizes a long-lived UI, API, configuration, persisted
  state, public export, source type, or extension-point category, and
  implementation is about to expose an exact variant that remains ambiguous
severity: warn
anti_patterns:
  - id: agentic-coding.implementation.speculative-public-surface
    name: Speculative public surface
    description: Generalizing one requested variant into a broader public capability, which creates unsupported compatibility and maintenance obligations.
    severity: warn
---

## When to apply

Apply at the last implementation decision before exposing a variant within a product-surface category that accepted scope already authorizes. An entirely unplanned surface, or one that materially changes scope, risk, or evidence needs, is a near miss: pause and replan from that drift. An internal refactor that preserves all observable surfaces is also a near miss.

## Guidance

Identify the authority for the accepted surface category, then compare the exact variants it supports with what the implementation would expose. Decide which proven variant boundary to admit or leave the ambiguous variant unexposed pending confirmation. The output is one bounded surface decision; do not infer neighboring modes merely because the implementation can generalize cheaply.

## Anti-pattern

Turning an authorized two-state notification preference into arbitrary channel identifiers, per-channel schemas, and a public extension interface because a generic abstraction appears cleaner.

## Why

Public and persisted surfaces acquire compatibility, documentation, validation, migration, and security obligations as soon as consumers can rely on them. Confirming the exact variant before exposure prevents implementation convenience from silently becoming product policy.

## Exceptions and boundaries

Compatibility with an already published contract, an approved migration, or an explicit platform requirement may require a broader surface than the immediate use case. In that case preserve the established obligation and record its authority. This Practice does not prohibit future-facing design internally; it constrains what becomes externally dependable now.

## Example

Accepted scope authorizes a display-density preference and names compact and comfortable modes. The agent exposes only those values and leaves custom style tokens unexposed pending authority. The observable result is a bounded preference contract.
