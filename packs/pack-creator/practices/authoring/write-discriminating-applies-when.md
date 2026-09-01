---
anti_patterns:
  - description: Naming a broad area or activity because it improves apparent recall, even though the wording gives retrieval no basis for choosing this Practice over its neighbors.
    id: pack-creator.authoring.topic-label-trigger
    name: Topic label used as a trigger
    severity: warn
applies_when: a Practice has a settled decision and the author must write when that one decision arises without also selecting neighboring Practices
id: pack-creator.authoring.write-discriminating-applies-when
severity: warn
stage: authoring
tech_stack:
  - lorelum-pack-authoring
title: Write a Trigger That Selects One Practice
---

## When to apply

Apply after one Practice decision is defined and before treating its `applies_when` as finished. The
question is when this specific decision arises, not which broad topic the Practice discusses.
Pack-wide retrieval moments belong in Pack design, while the actions and stopping point after
retrieval belong in Guidance.

## Guidance

Name the event or choice facing the reader, the affected object, and the fact that makes this
Practice relevant now. When a neighboring Practice could match, record a near-miss in the retrieval
fixture or authoring notes, then put only the fact that distinguishes the two decisions into
`applies_when`. Remove domain labels that do not narrow the decision. Stop with a trigger that lets
a cold reader explain both when to retrieve this Practice and when to retrieve its nearest neighbor
instead.

## Anti-pattern

A security Pack is meant to help SaaS teams avoid credential incidents. Its sources include separate
failures in token storage, rotation, and request validation. The author writes "applies when working
on authentication" for every related Practice because broad wording appears likely to retrieve them
all. The result has high apparent recall but no signal for choosing the token-storage rule when an
engineer is deciding where a new third-party token will be persisted.

## Why

Retrieval can select one Practice reliably only when its trigger names a distinguishable decision. A
topic label makes neighboring Practices compete for the same query and adds irrelevant guidance at
the moment of action.

## Exceptions and boundaries

A Practice may cover several technologies or roles when they face the same decision under the same
conditions. Do not add implementation instructions merely to make the trigger more specific. If two
different decisions remain in one trigger, split the Practice before polishing the wording.

## Example

A database-operations Pack contains a Practice about adding an index during a live schema change.
Migration records show that the risky decision occurs when a proposed index may scan or lock a
populated table, not during every database change. The author writes the trigger around that
condition and excludes ordinary metadata-only migrations, leaving index construction steps to
Guidance.
