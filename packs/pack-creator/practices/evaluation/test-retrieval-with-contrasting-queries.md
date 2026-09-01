---
anti_patterns:
  - description: Testing only queries that repeat a Practice title or wording makes retrieval look accurate while hiding near-miss and nearest-neighbor queries that select the wrong guidance.
    id: pack-creator.evaluation.positive-query-only-confidence
    name: Confidence from positive queries alone
    severity: warn
applies_when: a Practice set is ready for retrieval evaluation, and the author must determine whether each Practice is selected for its intended decision rather than for broad topic words shared with neighboring guidance
id: pack-creator.evaluation.test-retrieval-with-contrasting-queries
severity: warn
stage: evaluation
tech_stack:
  - lorelum-pack-authoring
title: Test Retrieval with Queries That Should and Should Not Match
---

## When to apply

Apply when the canonical Practices are stable enough to test selection behavior. The decision is
whether the queries distinguish one Practice from plausible alternatives. Structural catalog
coverage and content review are separate checks; this Practice requires observations from the
retrieval system being evaluated.

## Guidance

For each important Practice, prepare a small contrasting set: a direct query for its decision, a
natural paraphrase without copied title words, a near-miss that should not select it, and a query
aimed at the closest neighboring Practice. State the expected selection or non-selection before
running the queries. Use realistic wording from the people or Agents expected to retrieve the Pack,
then inspect both missing results and convincing wrong results. Revise triggers or split/merge
content only when the observed confusion reflects the Practice design rather than a known
retrieval-system defect. Stop when the important neighbors are distinguishable on representative
contrasts; adding many easy positive queries does not strengthen the conclusion.

## Anti-pattern

An author evaluates a security-logging Pack. The repository contains separate Practices for choosing
fields during event design and for protecting sensitive values during log emission. To finish
quickly, the author tests “which fields should security logs contain?” and several title-like
variations. The correct Practice always appears, which seems persuasive. No query asks “this
existing logger exposes session tokens—what should I change?” so the evaluation never reveals that
the field-design Practice outranks the redaction Practice whenever both mention “security log
fields.”

## Why

A positive query shows that a Practice can be found; it does not show that retrieval knows when that
Practice is the wrong answer. Contrasting queries reveal whether triggers and neighboring guidance
carry enough information to make a useful choice rather than matching a shared topic.

## Exceptions and boundaries

Early drafts may use a few manual contrasts before automated evaluation exists, but label those
results as limited observations. Exact expected ranking is unnecessary when the product contract
only requires the right small set, yet obviously harmful neighbors should still be rejected. Query
count, catalog coverage, and fixture validity do not by themselves prove retrieval quality.

## Example

An operations Pack has separate Practices for setting a latency alert threshold and for diagnosing
an alert that is already firing. The author writes four expectations for the threshold Practice:
“choose a p95 threshold” should select it; “how sensitive should this latency alarm be?” should also
select it; “the alarm is firing after a deploy—what changed?” should not; and “investigate repeated
latency pages” should prefer the diagnosis Practice. Running those contrasts exposes one ambiguous
`applies_when`, which the author narrows before stopping the evaluation.
