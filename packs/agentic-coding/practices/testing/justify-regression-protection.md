---
id: agentic-coding.testing.justify-regression-protection
title: Require Evidence for Regression Protection
stage: testing
tech_stack:
  - agentic-coding
applies_when: >-
  the agent is about to add a long-lived negative test, regression test, lint
  rule, or delivery gate after a reproduced and classified regression or an
  authoritative correction, and must decide whether preventing recurrence is a
  durable contract
severity: warn
anti_patterns:
  - id: agentic-coding.testing.memorialized-transient-mistake
    name: Memorialized transient mistake
    description: Turning an agent's rejected or one-off behavior into a permanent negative assertion or gate without a contract or evidenced recurrence risk, which creates corrective residue.
    severity: warn
---

## When to apply

Apply before making a classified regression or authoritative correction a permanent part of the project’s verification surface. The trigger is the durability decision, not ordinary positive coverage of a current requirement. An unclassified failure is a near miss and must be classified before regression protection is considered. A security prohibition, compatibility boundary, or explicit acceptance condition already documented as durable is also a near miss because its justification is established.

## Guidance

Identify the proposed protection and require at least one durable basis: an explicit contract, an observable absence requirement, a real regression with credible recurrence, or a high-impact safety, privacy, compatibility, or data-integrity boundary. Decide to keep, narrow, time-bound, or omit the protection based on that basis. The output is one protection decision with its justification; a recent mistake alone is not evidence that the project needs a permanent rule.

## Anti-pattern

After removing unrequested text, adding a permanent assertion that the exact text never appears again, even though the user only asked to restore the original design and established no new prohibition.

## Why

Tests and gates convert history into future maintenance obligations. Requiring a durable reason preserves protections that prevent meaningful harm while avoiding a growing rule set that memorializes every discarded exploration or local correction.

## Exceptions and boundaries

Unauthorized access, secret exposure, destructive data loss, regulatory violations, and published compatibility breaks can warrant protection after a single credible incident because the failure cost is high. Temporary safeguards may also be appropriate during a migration if their removal condition is explicit. Do not reject a protection merely to minimize test count or diff size.

## Example

An agent removes an unrequested tooltip and declines to add a “tooltip must never exist” test. It does add a denial-path test for unauthorized access because absence of access is an explicit security contract.
