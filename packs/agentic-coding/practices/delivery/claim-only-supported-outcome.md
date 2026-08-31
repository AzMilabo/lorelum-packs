---
id: agentic-coding.delivery.claim-only-supported-outcome
title: Claim Only the Supported Outcome
stage: delivery
tech_stack:
  - agentic-coding
applies_when: the agent is about to say that work is complete, fixed, accepted, deployed, pushed, or verified, and the available evidence may cover only a narrower artifact state or technical slice
severity: warn
anti_patterns:
  - id: agentic-coding.delivery.capability-inflation
    name: Technical slice inflated to capability
    description: Using a broad completion verb for evidence that covers only a component or local check causes recipients to rely on behavior that was never verified.
    severity: warn
---

## When to apply

Apply at the moment of forming a completion or status claim from the evidence currently available. Do not apply merely because residual work exists; residual reporting is a separate decision unless it changes the supported wording.

## Guidance

Identify the artifact state, behavior, environment, and scope directly supported by current evidence. Choose a verb and object no broader than that boundary, and distinguish a technical slice from an end-user capability when the latter spans additional flows. Stop with one calibrated outcome statement; omit unverified implications rather than softening them with confidence language.

## Anti-pattern

Saying "webhook delivery is accepted" because one event arrives and a focused handler test passes, even though retry exhaustion and invalid-signature rejection were not exercised.

## Why

Recipients often treat completion verbs as permission to merge, release, or stop investigating. Matching the sentence to the proof prevents a locally true result from triggering decisions that assume the whole capability exists.

## Exceptions and boundaries

Use the project's formally defined completion vocabulary when it has explicit gates, but still state when a gate was not run or refers to a different artifact state. Do not weaken a confirmed full-capability result into vague language merely because several independent evidence items support it.

## Example

Instead of "the search rollout is complete," report "query ranking passed the sampled relevance cases on the current index; failover behavior was not exercised."
