---
id: agentic-coding.correction.restore-authoritative-baseline
title: Restore the Authoritative Baseline
stage: correction
tech_stack:
  - agentic-coding
applies_when: an authoritative user correction, accepted scope change, or rejection of unrequested behavior has invalidated the current direction, and the agent is about to continue from assumptions formed before that correction
severity: warn
anti_patterns:
  - id: agentic-coding.correction.correction-overreach
    name: Correction promoted to prohibition
    description: Turning removal of one unsupported behavior into a new permanent negative contract preserves the original drift in tests, rules, or documentation instead of restoring the real requirement.
    severity: warn
---

## When to apply

Apply when authoritative input has already corrected the route and pre-correction assumptions may still shape implementation, tests, or plans. Do not apply to an ordinary source conflict that has not yet been resolved, or to feedback that remains an unvalidated finding.

## Guidance

Return to the authoritative goal, acceptance criteria, and explicit constraints now in force. Remove or revise assumptions, work items, implementation, and protection whose only basis was the superseded interpretation, while preserving independently justified requirements. Stop with a baseline that distinguishes restoration of the prior requirement from any newly accepted scope.

## Anti-pattern

After removing unrequested helper text, adding a permanent negative test and design rule forbidding such text everywhere, even though the correction only restored the supplied design.

## Why

Corrections fail when obsolete reasoning survives in downstream artifacts. Rebuilding from current authority prevents both continued drift and the mirror-image error of converting one rejected experiment into a lasting product constraint.

## Exceptions and boundaries

A correction can establish a new durable contract when the authority explicitly says so, or when safety, privacy, compliance, data integrity, or compatibility independently requires protection. Preserve unaffected work rather than treating every correction as permission to discard the whole implementation.

## Example

The user rejects an invented weekly email and confirms that the request was only for an on-screen status badge. The agent removes the scheduler and email tests, keeps the badge, and does not add a rule forbidding future notification features.
