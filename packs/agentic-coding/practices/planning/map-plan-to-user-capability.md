---
id: agentic-coding.planning.map-plan-to-user-capability
title: Map the Plan to User Capability
stage: planning
tech_stack:
  - agentic-coding
applies_when: >-
  a multi-file or multi-layer implementation plan is about to be finalized, and
  its technical work items have not yet been checked as a complete path through
  the requested user capability or preserved behavior
severity: warn
anti_patterns:
  - id: agentic-coding.planning.component-completion-substitution
    name: Component completion substitution
    description: >-
      The agent treats completion of visible components or technical layers as
      completion of the capability, leaving cross-layer behavior such as
      authorization, persistence, or recovery absent from the plan.
    severity: warn
---

## When to apply

Apply when a plan spans components, services, storage, policies, or other boundaries and may be technically complete item by item while missing part of the user flow. For an internal refactor, the capability is the behavior that must remain unchanged. If implementation is finished and the question is which acceptance conditions existing evidence covers, perform evidence mapping instead.

## Guidance

Trace the requested capability from its initiating actor and action through every necessary boundary to the observable result. Map each planned item to the part of that path it enables, and identify any required step with no owner. Resolve uncovered steps or explicitly narrow the promised capability; do not count a layer's completion as proof that the path is whole. Stop when the plan has an end-to-end capability map with no unexplained required gaps.

## Anti-pattern

A plan covers an inventory-transfer request and confirmation screen but omits authorization and stock reservation. Each named component can be finished while the requested “authorized staff can move available stock without overselling” capability still fails.

## Why

Technical task lists encourage local completion signals. Mapping them to an actor-to-outcome path exposes missing handoffs and domain semantics before implementation makes the partial design expensive to change.

## Exceptions and boundaries

A deliberately staged technical slice may cover only part of the capability when that limitation is explicit and no full-capability claim is planned. Infrastructure or refactoring work with no direct user interface should map to the stable behavior or operational outcome it preserves, not invent a fictional end user.

## Example

For an inventory transfer, map initiation, authorization, reservation, commit, and refreshed stock totals to the operator outcome. If the plan ends at request creation, add the missing reservation and commit path or narrow the stated delivery before work begins.
