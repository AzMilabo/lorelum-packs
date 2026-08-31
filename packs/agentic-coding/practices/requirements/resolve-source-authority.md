---
id: agentic-coding.requirements.resolve-source-authority
title: Resolve Authority Across Conflicting Sources
stage: requirements
tech_stack:
  - agentic-coding
applies_when: >-
  requirements are being established and current instructions, specifications,
  summaries, code, or prior decisions disagree, before one of them is used to
  define intended behavior
severity: warn
anti_patterns:
  - id: agentic-coding.requirements.promote-convenient-source
    name: Convenient source promotion
    description: >-
      The agent treats the most recent, detailed, or implementation-friendly
      source as authoritative without checking its role or status, causing stale
      behavior or speculation to become a requirement.
    severity: warn
---

## When to apply

Apply when two or more sources imply different intended behavior and the agent must choose a requirement baseline. A source may be a current user instruction, adopted specification, issue, decision record, code state, summary, or earlier conversation. If the sources agree and the question is only whether existing code can be reused, inspect the implementation instead.

## Guidance

For the disputed point, classify each relevant source as current authority, historical or observed fact, unconfirmed interpretation, or superseded evidence. Use explicit adoption, recency of an authorized correction, and the project's stated governance to choose the current authority; neither detail nor chronology alone is sufficient. Record the resulting authority decision and the conflict it resolves. If no available rule can decide a material product behavior, surface that unresolved choice to an authorized person and stop before encoding it.

## Anti-pattern

A compact summary says audit records expire after one year, while the adopted retention policy requires seven years. Continuing from the summary because it is shorter promotes a derivative source over the requirement authority.

## Why

Separating authority from observation prevents current code, old decisions, and agent-generated explanations from acquiring requirement status through repetition. It also makes later corrections local: the superseded source remains useful as history without controlling new work.

## Exceptions and boundaries

An emergency safety or data-protection constraint may temporarily override a lower-authority product instruction when the governing policy explicitly grants that precedence; record the override and its scope. This Practice decides which source defines intent. It does not decide whether an implementation should be reused or whether a new design is preferable.

## Example

The current cleanup job deletes audit records after one year, but the approved retention policy requires seven years. Record the policy as requirement authority and the job schedule as current-state evidence, not as the target behavior.
