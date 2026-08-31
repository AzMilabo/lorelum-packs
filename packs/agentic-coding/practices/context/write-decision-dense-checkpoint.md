---
id: agentic-coding.context.write-decision-dense-checkpoint
title: Write a Decision-Dense Checkpoint
stage: context
tech_stack:
  - agentic-coding
applies_when: a long pause, context reduction, or session boundary is imminent, and the agent must create a durable checkpoint without carrying exploratory noise into the resumed task
severity: warn
anti_patterns:
  - id: agentic-coding.context.recency-biased-checkpoint
    name: Recency-biased checkpoint
    description: Preserving the latest logs and implementation details while omitting authoritative goals, rejected assumptions, open acceptance, or evidence limits makes recent activity look more important than durable truth.
    severity: warn
---

## When to apply

Apply before a known interruption or context boundary when another reasoning pass will need a compact recovery artifact. Do not apply after context has already been lost; at that point the task must be re-grounded from durable sources rather than trusting a newly reconstructed checkpoint.

## Guidance

Write one checkpoint containing the current goal, authoritative sources, acceptance boundary, accepted decisions, unfinished scope, still-valid evidence, and material risks or unknowns. Reduce rejected options, failed experiments, and long outputs to only the conclusions that constrain future decisions, and label uncertainty rather than converting it into fact. Stop when the checkpoint can direct re-reading and continuation without preserving the entire process transcript.

## Anti-pattern

Recording every file touched and recent test log while omitting that authorization rejection remains unverified or that the apparent domain model was only an unconfirmed implementation assumption.

## Why

Future reasoning is steered by what the checkpoint makes salient. Preserving decision inputs and unresolved boundaries while compressing exploration reduces contamination without sacrificing the facts needed to continue correctly.

## Exceptions and boundaries

Retain full logs separately when incident response, audit, legal, or reproducibility requirements demand them; the checkpoint should point to that evidence rather than embed it. Very short, stateless tasks may need only a sentence if there is no meaningful decision state to preserve.

## Example

A checkpoint says that the goal is user-level role management, names the current specification, records the accepted aggregation decision, notes that denial behavior is unverified, and links the latest valid results. It reduces three failed UI approaches to "rejected because they split one user across rows."
