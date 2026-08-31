---
id: agentic-coding.recovery.reground-after-context-loss
title: Reground After Context Loss
stage: recovery
tech_stack:
  - agentic-coding
applies_when: work is resuming after context reduction, interruption, or a same-agent session resume, and the agent is about to edit or declare status using a summary whose claims have not been checked against durable task state
severity: warn
anti_patterns:
  - id: agentic-coding.recovery.summary-as-authority
    name: Summary used as authority
    description: Continuing directly from a condensed narrative can preserve stale assumptions, obsolete scope, and inflated completion claims that the durable requirements and current artifact contradict.
    severity: warn
---

## When to apply

Apply after context has been reduced or the same agent's session has resumed, before substantive editing or status claims rely on the surviving summary. A cross-agent transfer is a near miss and requires validating the handoff claims against current authority, artifacts, and evidence. Do not apply before an interruption when the task still has full context; create a durable checkpoint for that moment instead.

## Guidance

Use the summary only to locate the authoritative task sources, accepted plan or decisions, current artifact or diff, and recorded evidence. Re-read those items, compare them with the summary, discard superseded assumptions, and state the current goal, unfinished boundary, valid evidence, and next justified action. Stop with a re-grounded working state before implementation continues.

## Anti-pattern

Accepting a summary sentence that says "feature complete," then continuing with cleanup even though the current acceptance criteria and diff show that the authorization flow was never implemented or verified.

## Why

Summaries optimize continuity, not authority, and can overrepresent recent implementation detail. Re-grounding restores the decision inputs that determine correctness before a compressed error becomes the premise for more work.

## Exceptions and boundaries

A trivial stateless task may require only a quick comparison with its current artifact. When durable sources conflict with each other, pause for authority resolution rather than selecting the version that best matches the summary.

## Example

After resuming a parser refactor, the agent reopens the grammar requirements and current diff. It finds that core syntax checks remain valid but malformed-input recovery was never exercised, changes the state from "complete" to "core syntax verified," and continues from that corrected boundary.
