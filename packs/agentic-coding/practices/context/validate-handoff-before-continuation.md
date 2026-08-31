---
id: agentic-coding.recovery.validate-handoff-before-continuation
title: Validate Handoffs Before Continuing
stage: recovery
tech_stack:
  - agentic-coding
applies_when: another agent, contributor, or delegated task has returned conclusions or completion status, and the receiving agent is about to make a dependent decision without reconciling them with current authority, artifacts, and evidence
severity: warn
anti_patterns:
  - id: agentic-coding.recovery.handoff-as-proof
    name: Handoff treated as proof
    description: Treating a concise handoff as verified state lets omitted limits, stale artifact references, or unsupported conclusions become premises for the receiving agent's next work.
    severity: warn
---

## When to apply

Apply at a cross-agent or cross-contributor information boundary before the receiver acts on a reported finding, result, or completion status. Do not apply merely because the same agent is resuming after context loss, or when the handoff contains no conclusion relevant to the next decision.

## Guidance

Identify the handoff claims that the next action depends on, then compare them with the authoritative requirement, current artifact state, and cited evidence. Accept, narrow, reject, or escalate each dependent claim and discard assumptions made stale by concurrent changes. Stop with a validated handoff disposition and a corrected next action.

## Anti-pattern

Continuing from "all checks pass" when the handoff cites only component tests and the current branch has since changed the integration path required by acceptance.

## Why

Handoffs compress both evidence and uncertainty, while artifacts may change independently. Validation keeps delegation useful without allowing confidence, omission, or timing differences to propagate into the main task as false shared state.

## Exceptions and boundaries

Low-impact exploratory suggestions can remain explicitly provisional until they become decision inputs. An authoritative scope change delivered through a handoff should be processed as changed authority, not accepted merely because another agent reported it.

## Example

A delegated task reports that installation is verified. The receiver confirms the cited local install result but finds no upgrade evidence, narrows the claim to fresh installation, and keeps upgrade verification as the next action.
