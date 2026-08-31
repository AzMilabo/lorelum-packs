---
id: agentic-coding.implementation.confirm-product-surface-expansion
title: Confirm Any Product Surface Expansion
stage: implementation
tech_stack:
  - agentic-coding
applies_when: >-
  implementation is about to add a long-lived UI element, API, configuration,
  persisted state, public export, source type, or extension point whose exact
  variant is not clearly established by the accepted scope
severity: warn
anti_patterns:
  - id: agentic-coding.implementation.speculative-public-surface
    name: Speculative public surface
    description: Generalizing one requested variant into a broader public capability, which creates unsupported compatibility and maintenance obligations.
    severity: warn
---

## When to apply

Apply at the last implementation decision before introducing or broadening a surface that users, integrations, stored data, or downstream code may depend on. It is narrower than general scope review: the distinguishing condition is a new long-lived product or extension contract. An internal refactor that preserves all observable surfaces is a near miss.

## Guidance

Identify the authoritative requirement or confirmed decision for the proposed surface, then compare its exact supported variants with what the implementation would expose. Decide to admit the proven variant, narrow the design to it, or defer the expansion for confirmation. The output is one bounded surface decision; do not infer neighboring modes merely because the implementation can generalize cheaply.

## Anti-pattern

Turning a requirement for one configurable provider into arbitrary provider URLs, local files, multiple protocols, or a public plugin interface because a generic abstraction appears cleaner.

## Why

Public and persisted surfaces acquire compatibility, documentation, validation, migration, and security obligations as soon as consumers can rely on them. Confirming the exact variant before exposure prevents implementation convenience from silently becoming product policy.

## Exceptions and boundaries

Compatibility with an already published contract, an approved migration, or an explicit platform requirement may require a broader surface than the immediate use case. In that case preserve the established obligation and record its authority. This Practice does not prohibit future-facing design internally; it constrains what becomes externally dependable now.

## Example

A task requires selecting one named remote catalog. Instead of accepting every URL scheme, the agent exposes only the confirmed catalog identifier and defers arbitrary locators. The observable result is a narrower public input contract.
