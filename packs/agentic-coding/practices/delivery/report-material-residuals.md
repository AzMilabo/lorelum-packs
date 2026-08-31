---
id: agentic-coding.delivery.report-material-residuals
title: Report Only Material Residuals
stage: delivery
tech_stack:
  - agentic-coding
applies_when: delivery or handoff is imminent, known remaining work, risk, plan deviation, or verification limitation exists, and the agent must decide what the next decision-maker needs to know
severity: warn
anti_patterns:
  - id: agentic-coding.delivery.residual-log-dump
    name: Residual log dump
    description: Reporting every explored path and transient failure obscures the unresolved items that can change the recipient's next action, release decision, or recovery path.
    severity: warn
---

## When to apply

Apply when a delivery or handoff has at least one known residual that may affect what happens next. Do not add an empty residuals section when nothing material remains, and do not use this Practice to restate the evidence-supported completion claim.

## Guidance

Select only unresolved work, risk, deviation, or verification limits that could change the recipient's next decision. For each selected residual, state its present impact and the minimum reproduction, mitigation, or rollback information needed to act. Stop when the recipient can choose the next step without replaying the exploration history.

## Anti-pattern

Hiding an unverified migration behind pages of command output, discarded hypotheses, and harmless warnings, or reporting all of that noise as if every item carried equal risk.

## Why

Material residuals preserve decision continuity; process exhaust consumes attention and can bury the actual blocker. A concise, actionable record lets the next owner assess risk without mistaking verbosity for completeness.

## Exceptions and boundaries

Regulated, forensic, incident, or audit workflows may require a complete retained log, but the operational handoff should still distinguish decision-relevant residuals from the archive. A transient failure that was reproduced, explained, and cleared is material only if recurrence or uncertainty can affect the next action.

## Example

A handoff reports that the data migration was not exercised against a production-sized copy, states the possible timeout impact, and gives the rollback checkpoint. It omits unrelated failed searches and superseded debugging guesses.
