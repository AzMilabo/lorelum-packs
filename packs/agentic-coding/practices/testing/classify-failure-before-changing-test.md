---
id: agentic-coding.testing.classify-failure-before-changing-test
title: Classify Failures Before Changing Tests
stage: testing
tech_stack:
  - agentic-coding
applies_when: >-
  a test, lint, type, build, or validation check has failed, and the agent is
  about to change production code, test expectations, or configuration before
  establishing what kind of failure occurred
severity: warn
anti_patterns:
  - id: agentic-coding.testing.test-accommodation-before-diagnosis
    name: Test accommodation before diagnosis
    description: Updating the failing expectation to match current output before determining whether the product, test, environment, or baseline is wrong, which can erase evidence of a real defect.
    severity: warn
---

## When to apply

Apply after a check fails and before editing either the implementation or its verifier. The needed output is a cause classification: product defect, outdated test or contract, environment or nondeterminism, or unrelated pre-existing baseline. A failure with already decisive evidence and an agreed classification is a near miss; proceed with the corresponding fix.

## Guidance

Reproduce the smallest relevant failure and compare its observed behavior with the authoritative requirement and the state being tested. Gather only enough additional evidence to distinguish the candidate classes, then record the classification and the evidence that rules out the nearest alternative. Choose the change that follows from that classification. If the evidence remains ambiguous, keep the test and behavior unchanged while escalating the uncertainty rather than guessing through edits.

## Anti-pattern

Seeing that a redesigned screen breaks a test, immediately updating selectors and expected rows to fit the new screen, and only later asking whether the redesigned behavior still satisfies the requirement.

## Why

A failing check is evidence of disagreement, not evidence of which side is wrong. Classification preserves that signal long enough to locate the disagreement and prevents test edits from laundering implementation drift into apparent correctness.

## Exceptions and boundaries

Contain active security, data-loss, or production incidents before completing a full diagnosis when delay increases harm, while preserving evidence for follow-up. Clearly corrupt generated artifacts or unavailable infrastructure may be repaired once their cause is directly established. A user-approved requirement change can make a test outdated, but the approval must be the basis for that classification.

## Example

A search test fails after results are grouped differently. The agent checks the requirement and finds grouping was never changed; it classifies the failure as a product defect and fixes grouping instead of rewriting the expectation.
