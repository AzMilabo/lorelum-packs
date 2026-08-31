---
id: agentic-coding.verification.bind-evidence-to-artifact-state
title: Bind Evidence to Artifact State
stage: verification
tech_stack:
  - agentic-coding
applies_when: verification evidence is being recorded or reused, and the agent must decide whether it still applies after code, configuration, environment, or generated artifacts may have changed
severity: warn
anti_patterns:
  - id: agentic-coding.verification.stale-proof-carryover
    name: Stale proof carryover
    description: Reusing a previous pass without identifying the artifact state and conditions it covered lets later changes inherit proof they never received.
    severity: warn
---

## When to apply

Apply when preserving, citing, or reusing evidence across edits, configuration changes, generated outputs, environment changes, or time-sensitive observations. Do not apply merely because an acceptance criterion lacks evidence; this Practice decides freshness, not how to close a known gap.

## Guidance

For each evidence item, identify the artifact state it examined, the relevant environment or configuration, when it was obtained, and its behavioral scope. Compare those bindings with the current state and invalidate only the evidence whose conclusion could be changed by the difference. Stop with a current, stale, or unaffected status for the evidence item.

## Anti-pattern

Carrying "review passed" or "tests passed" into a completion claim after the reviewed diff or tested configuration changed, without checking whether the old result still describes the current artifact.

## Why

Evidence is a relationship between an observation and a particular state, not a permanent property of a task. Explicit bindings prevent stale results from silently proving new work while preserving unaffected evidence instead of forcing indiscriminate reruns.

## Exceptions and boundaries

Stable facts whose premises are unchanged can remain valid, even when unrelated files change. Security-sensitive, destructive, release, or environment-dependent claims may require stricter freshness rules defined by the authoritative contract.

## Example

A focused parser test is bound to revision A and remains relevant after a documentation-only edit. A generated package created at revision A is rebuilt after parser code changes to revision B, because the old artifact no longer represents the current source.
