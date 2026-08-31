---
id: agentic-coding.review.validate-findings-before-action
title: Validate Findings Before Taking Action
stage: review
tech_stack:
  - agentic-coding
applies_when: a human, agent, analysis tool, or review has raised a finding, and the agent is about to change the artifact before confirming the finding against current authority and state
severity: warn
anti_patterns:
  - id: agentic-coding.review.finding-as-fact
    name: Finding treated as fact
    description: Acting on a plausible review statement without checking the current requirement and artifact can fix a stale, mis-scoped, or requirement-conflicting problem into the product.
    severity: warn
---

## When to apply

Apply when an external finding is about to drive a code, test, document, or plan change. Do not apply to a defect already reproduced against the current artifact and current contract unless new evidence puts that conclusion in doubt.

## Guidance

Compare the finding with the authoritative requirement, the current artifact state, its claimed contract, and relevant observations. Classify it as confirmed, unconfirmed, or requiring an authority decision, and attach only the next action warranted by that classification. Stop before editing when the finding remains unconfirmed or would change the accepted requirement.

## Anti-pattern

Accepting "remove the custom source to reduce complexity" as a defect and deleting it, even though the current requirement explicitly needs that source and the review supplied no contrary authority.

## Why

Review findings are hypotheses whose quality and freshness vary. Validation keeps useful findings actionable while preventing persuasive wording, stale context, or proxy goals such as smaller diffs from silently overriding the task.

## Exceptions and boundaries

Immediately contain an actively exploitable security issue or destructive failure when delay would increase harm, then complete validation before making the containment permanent. A maintainer decision that legitimately changes scope should be treated as new authority, not merely as a confirmed technical finding.

## Example

A reviewer reports that a decoder accepts invalid input. The current code and a focused reproduction confirm the case, so the finding is marked confirmed and fixed locally; a separate suggestion to remove a required input mode is held for an authority decision.
