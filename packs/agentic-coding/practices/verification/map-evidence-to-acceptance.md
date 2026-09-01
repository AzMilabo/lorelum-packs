---
anti_patterns:
  - description: Treating a long list of commands, tests, or inspections as proof of acceptance without mapping results to criteria hides unsupported capabilities behind visible activity.
    id: agentic-coding.verification.coverage-by-activity
    name: Coverage by activity
    severity: warn
applies_when: implementation is ready for verification, actual checks or observations are available, and the agent is about to decide which acceptance criteria those results cover
id: agentic-coding.verification.map-evidence-to-acceptance
severity: warn
stage: verification
tech_stack:
  - agentic-coding
title: Map Evidence to Acceptance Criteria
---

## When to apply

Apply after checks or observations exist and before deciding that acceptance has been demonstrated.
The decision is which current criterion each result actually supports. Planning future evidence
happens before implementation; checking whether a result is still fresh is a separate state-binding
decision; resolving a row left uncovered happens after this map exposes it.

## Guidance

Copy the current acceptance criteria from the user request, accepted issue, or specification. Beside
each one, name the exact test result, inspected file, or direct observation that exercised it,
including the behavior and environment actually covered. One result may support several criteria
only when it really observed each outcome. Write “not covered” or “partly covered” when a result
stops short. Stop with this criterion-by-criterion table or list; do not fill empty rows with
confidence, test counts, or nearby successes.

## Anti-pattern

The user asks for booking submission to issue one reservation even when a request is retried. The
repository has green calculation tests, a full build, static checks, and one successful booking
demonstration. Because the log is substantial and every command is green, the agent reports
verification complete. None of those results retries a submission, so the no-duplicate requirement
disappears behind the activity summary.

## Why

Verification results have narrower meaning than their command names suggest. Mapping makes that
meaning explicit, exposes silent gaps, and lets reviewers challenge a particular criterion-to-result
relationship instead of interpreting a dense log as a general proof.

## Exceptions and boundaries

A single end-to-end observation may cover several criteria when it really includes them; do not
duplicate work to force one result per row. Mandatory gates may be recorded even when they do not
directly prove a user capability, but label their role. If the user request, accepted issue, and
specification do not agree on acceptance, ask which one controls the work before inventing criteria.
This Practice produces the map, not the final delivery wording.

## Example

The user asks for a report with required fields, readable pages, and a file that opens on the target
phone. The repository has a schema test, rendered page images, a successful phone download, and a
green build. The agent maps the schema result to required fields, the image inspection to
readability, and the phone observation to delivery and opening. It records the build only as a
required gate. Because no check interrupted and resumed a download, offline retry remains explicitly
uncovered.
