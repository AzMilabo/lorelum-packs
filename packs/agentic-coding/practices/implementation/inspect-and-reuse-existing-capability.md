---
id: agentic-coding.implementation.inspect-and-reuse-existing-capability
title: Reuse Existing Capability Before Building
stage: implementation
tech_stack:
  - agentic-coding
applies_when: >-
  implementation is about to add a helper, layer, or mechanism, and the agent
  must decide whether the runtime, a dependency, or a nearby module already
  provides the required capability under the current constraints
severity: warn
anti_patterns:
  - id: agentic-coding.implementation.reflexive-reimplementation
    name: Reflexive reimplementation
    description: Building a familiar capability from memory before inspecting relevant existing code or dependencies, which duplicates behavior and creates another contract to maintain.
    severity: warn
---

## When to apply

Apply immediately before creating a new implementation for a capability that could plausibly exist in the runtime, declared dependencies, related modules, or their tests. This is a reuse decision, not a general search ritual. Do not apply when current evidence already establishes that the capability is intentionally new or that existing options cannot meet a required constraint.

## Guidance

Inspect the smallest evidence set that can answer the reuse question: the relevant module boundary, its call sites and tests, then the runtime or dependencies most likely to own the capability. Decide among direct reuse, a small adaptation, or a new implementation. Record the constraint that rules out each closer option. Stop searching once the evidence distinguishes those choices; the output is one reuse decision, not a catalog of alternatives.

## Anti-pattern

Writing a parser, validator, retry loop, cache, or abstraction from memory because it is easy to implement, then discovering that the project already carries an equivalent with different edge-case behavior.

## Why

Existing capabilities often encode compatibility, failure semantics, and maintenance ownership that are invisible in a fresh local implementation. Inspecting before building prevents parallel contracts and focuses new code only where the current requirement actually exceeds what already exists.

## Exceptions and boundaries

Do not reuse a capability merely because its name matches. A security boundary, license restriction, unsupported environment, unstable API, or proven semantic mismatch can justify a new implementation. Choosing among several already-feasible designs belongs to design selection; this Practice only establishes whether reuse is a valid first option.

## Example

Before adding custom version comparison, an agent finds that the project runtime already exposes comparison with the required prerelease semantics. The observable decision is “reuse the runtime function,” with no new comparator or wrapper.
