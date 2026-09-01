---
anti_patterns:
  - description: The agent treats a set of finishable components or layers as the complete capability because each has a clear task, leaving a cross-layer behavior or required rule with no owner.
    id: agentic-coding.planning.component-completion-substitution
    name: Component completion substitution
    severity: warn
applies_when: a multi-component or multi-layer implementation plan is about to be finalized without checking that its tasks form the complete requested behavior path
id: agentic-coding.planning.map-plan-to-user-capability
severity: warn
stage: planning
tech_stack:
  - agentic-coding
title: Map the Plan to User Capability
---

## When to apply

Apply when a plan spans interfaces, services, storage, policies, or other boundaries and may miss
part of the requested path. For an internal refactor, map the behavior that must remain unchanged.
If implementation is finished and evidence must be compared with acceptance, map evidence instead.

## Guidance

Trace the initiating action through every required boundary to the observable result. Map each task
to the step it enables and find required steps with no owner. Add the missing responsibility or
narrow the promised capability; layer completion does not prove the path is whole. Stop when the map
has no unexplained required gap.

## Anti-pattern

An inventory-transfer plan includes a request endpoint and confirmation screen, both straightforward
to build and test. It omits stock reservation between them because that responsibility sits in
another service. Every listed task can finish while two operators still oversell the same stock.

## Why

Technical task lists reward local completion. An actor-to-result map exposes missing handoffs before
partial implementation makes them expensive to repair.

## Exceptions and boundaries

A planned partial delivery may cover only part of the capability when that limit is explicit.
Infrastructure and refactoring work should map to the operational behavior they preserve rather than
inventing a fictional user.

## Example

A password-reset task enters a repository that already has token creation and validation, making a
token-only plan look nearly complete. The agent maps request, message delivery, token validation,
password update, and required session invalidation to secure account recovery. It adds the missing
update and invalidation work before coding instead of calling the token service the whole
capability.
