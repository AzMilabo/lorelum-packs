---
anti_patterns:
  - description: The author preserves separate, familiar rules because they came from different sources, even though readers describe both with the same query and cannot tell which action applies.
    id: pack-creator.design.neighbor-collision-by-label
    name: Familiar labels hide a retrieval collision
    severity: warn
applies_when: two or more atomic Practice drafts appear relevant to the same realistic query, and the author must distinguish their triggers and actions or merge them
id: pack-creator.design.separate-neighboring-triggers
severity: warn
stage: design
tech_stack:
  - lorelum-pack-authoring
title: Separate Practices That Compete for the Same Query
---

## When to apply

Apply after guidance has been split into atomic Practice drafts and two entries still seem
appropriate for the same request. Compare the exact decision each entry changes, not only its title
or domain. This Practice resolves competition between files; it does not decide the earlier question
of whether one draft contains several decisions.

## Guidance

Write one realistic positive query and one paraphrase for each draft, then use each other's positive
query as a near miss. State the different fact that selects one action over the other. Revise the
trigger, title, and guidance until a cold reader can route the cases. If no meaningful boundary
exists, merge the drafts or redefine the decisions instead of relying on subtle wording. Stop when
overlap means both decisions genuinely apply, not that either Practice could answer the same
question.

## Anti-pattern

A web-security Pack should help developers choose the right control for untrusted data. It contains
"Validate User Input" from an API guide and "Sanitize User Input" from a frontend review checklist.
Both say they apply when handling untrusted text, and keeping the familiar labels seems easier for
reviewers than challenging the sources. A developer asking how to safely display a profile name
retrieves both, one recommending rejection and the other vague cleaning, without learning that
output encoding at the HTML sink is the needed decision. The author should distinguish
trust-boundary validation from context-specific output encoding, or merge the entries if the Pack
cannot sustain that boundary.

## Why

Atomic files can still be poor retrieval targets when their selection conditions are
indistinguishable. A visible near-miss boundary reduces noisy retrieval and conflicting action.

## Exceptions and boundaries

Two Practices may correctly retrieve together when a situation contains two separate decisions. That
is not a collision if each Practice owns a different action and remains useful. Domain terms can
stay in titles when readers actually use them, but labels alone cannot carry the boundary.

## Example

A database-performance Pack should help engineers decide how to improve slow queries without adding
unjustified indexes. It has one Practice for deciding whether a new index is justified by a
recurring query pattern and another for checking the execution plan after an index or query changes.
A request proposing an index before implementation selects the first; a report that an existing
indexed query became slow selects the second. The author states those moments and actions
explicitly. A broad request covering both design and regression may retrieve both because both
decisions are present.
