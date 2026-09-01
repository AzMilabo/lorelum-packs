---
anti_patterns:
  - description: The author keeps several decisions together because one guide or repository module discusses them together, producing a polished Practice that is too broad for focused retrieval and too costly for readers who need only one choice.
    id: pack-creator.design.source-section-as-practice-boundary
    name: Source section used as the Practice boundary
    severity: warn
applies_when: a candidate Practice contains several actions or rules that could be needed by different queries, and the author must decide whether to split the content
id: pack-creator.design.decompose-one-decision-per-practice
severity: warn
stage: design
tech_stack:
  - lorelum-pack-authoring
title: Decompose Guidance into One Decision per Practice
---

## When to apply

Apply while turning candidate guidance into Practice files, when one draft changes more than one
decision. Decide whether the actions always arise together or should be independently retrievable.
After separate files exist, a different review checks whether their triggers still collide.

## Guidance

Underline the decision verbs in the draft. If a reader could reasonably need one action without the
others, give each decision its own trigger, guidance, failure mechanism, and boundary. Keep shared
evidence in provenance or links instead of using a source chapter as the file boundary. Recombine
pieces that make no independent choice and only repeat setup. Stop when each Practice can change one
decision without requiring unrelated guidance to be retrieved with it.

## Anti-pattern

A frontend-performance Pack should help teams prevent slow page loads. One internal guide covers
image sizing, cache policy, bundle splitting, and performance measurement in a single chapter, so
keeping them together preserves context and avoids repeated citations. The author creates "Optimize
Page Performance" with all four actions. A reviewer deciding whether an image variant is needed
receives cache and bundler guidance, while a query about cache policy may not retrieve the broad
title at all. The better design splits the independently triggered decisions and keeps the shared
guide as provenance.

## Why

Atomic Practices give retrieval a clear target and let readers act without carrying unrelated
instructions. Source structure describes how knowledge was documented, not necessarily how decisions
arise.

## Exceptions and boundaries

Steps that always occur as one decision and would be misleading alone can remain together. Do not
split a Practice merely to shorten it or create one file per paragraph. A multi-step check may still
be atomic when every step is required to answer the same question.

## Example

A database-change Pack should help engineers make schema changes that can recover without losing
existing data. One draft says to choose an online migration method, define rollback behavior, and
verify populated-data rollback before release. The author finds three distinct moments: selecting
the migration approach, deciding what rollback must preserve, and assessing whether evidence
supports release. Each can arise independently and has a different failure, so the author creates
separate Practices. The vendor migration guide remains a shared source rather than forcing the three
decisions back into one file.
