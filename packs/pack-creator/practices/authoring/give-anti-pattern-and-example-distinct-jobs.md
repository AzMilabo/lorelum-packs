---
anti_patterns:
  - description: Reversing the outcome of one scenario for the Example because consistency feels clear, while adding no new demonstration of how to apply the rule.
    id: pack-creator.authoring.duplicate-section-scenario
    name: Same scenario told twice
    severity: warn
applies_when: a Practice has both an Anti-pattern and an Example, and the author must check whether each section contributes different decision-relevant information
id: pack-creator.authoring.give-anti-pattern-and-example-distinct-jobs
severity: warn
stage: authoring
tech_stack:
  - lorelum-pack-authoring
title: Give the Anti-Pattern and Example Different Jobs
---

## When to apply

Apply after both sections have drafts. The Anti-pattern should expose the recurring wrong mechanism
and its consequence; the Example should demonstrate a correct application in a concrete situation.
This Practice checks their division of labor, not whether either scenario is realistic or
self-contained.

## Guidance

Summarize in one sentence what new information each section contributes. Keep the Anti-pattern
centered on temptation, wrong mechanism, and failure. Use the Example to show the correct action,
boundary, or output, preferably through a different situation that tests transfer. Remove repeated
setup and mirrored sentences. Stop when deleting either section would remove a distinct lesson.

## Anti-pattern

An operations Pack teaches teams to cap database connection demand. The author uses one checkout
surge for both sections: the Anti-pattern raises the pool limit until the database collapses, and
the Example repeats the same surge with a lower limit. Mirroring feels easy to compare, but both
sections teach only that one number was too high; neither shows how to apply the capacity boundary
elsewhere.

## Why

Two sections that repeat one scenario consume retrieval context without adding another decision
signal. Distinct roles let the reader recognize the failure and then transfer the correct action to
a new case.

## Exceptions and boundaries

Both sections may use the same domain when that domain is essential, but they should still
contribute different facts or decisions. A very short Practice may omit decorative detail; it should
not keep two sections whose only difference is positive versus negative wording.

## Example

A security Practice says to recheck authorization at the protected action. Its Anti-pattern explains
how caching team membership for an entire session seems fast but lets removed members retain access.
Its Example uses a different case: an export job verifies the requester's current role immediately
before reading an archive and denies the job after access is revoked. One section reveals the trap;
the other shows correct placement.
