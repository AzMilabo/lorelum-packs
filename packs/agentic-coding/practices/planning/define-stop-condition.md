---
anti_patterns:
  - description: The agent turns each attractive discovery into current work because it is nearby and technically coherent, allowing implementation momentum to move completion farther away.
    id: agentic-coding.planning.opportunity-driven-continuation
    name: Opportunity-driven continuation
    severity: warn
applies_when: accepted work is about to begin, nearby improvements could extend it indefinitely, and no explicit finish, defer, or replan boundary exists
id: agentic-coding.planning.define-stop-condition
severity: warn
stage: planning
tech_stack:
  - agentic-coding
title: Define Stop and Replanning Conditions
---

## When to apply

Apply before execution when cleanup, abstraction, or adjacent features could continue indefinitely.
Set the boundary before discoveries create momentum. If material drift has already appeared during
implementation, replan from the observed facts instead.

## Guidance

Write one boundary with the observable finish condition, nearby opportunities deferred, and material
signals that require replanning. Signals should be changes in scope, risk, authority, cost, or
evidence feasibility, not ordinary implementation detail. If completion cannot be stated, return to
the requirement instead of using "until it looks good." Stop when another person could decide
finish, defer, or replan from current facts.

## Anti-pattern

After adding the requested CSV export, the agent notices that the existing formatter interface could
support third-party formats. A plug-in registry, discovery mechanism, and compatibility tests all
look like coherent cleanup around the same code. Each addition is reasonable in isolation, but the
original export task never reaches a stable end.

## Why

A boundary prevents novelty and cleanup opportunities from redefining success. Replanning signals
preserve flexibility without turning every new idea into current work.

## Exceptions and boundaries

Incident response, safety containment, and research may use timeboxed or evidence-based stops.
Immediate containment can precede replanning when delay increases harm.

## Example

A task adds one documented search filter, while the search module also exposes hooks for saved
searches and query suggestions. The agent finishes when the field produces correct matching and
empty-result behavior, and defers both adjacent features. It replans only if the filter requires a
public index migration or invalidates the planned checks.
