---
id: agentic-coding.verification.map-evidence-to-acceptance
title: Map Evidence to Acceptance Criteria
stage: verification
tech_stack:
  - agentic-coding
applies_when: implementation is ready for verification, actual checks or observations are available, and the agent is about to decide which acceptance criteria those results cover
severity: warn
anti_patterns:
  - id: agentic-coding.verification.coverage-by-activity
    name: Coverage by activity
    description: Treating a list of executed checks as proof of acceptance without showing which criterion each result supports leaves untested capabilities hidden behind visible activity.
    severity: warn
---

## When to apply

Apply after implementation when concrete test results, inspections, or observations must be reconciled with the current acceptance criteria. Do not apply while merely choosing future checks; that is evidence planning, not a mapping of evidence already obtained.

## Guidance

Read the current acceptance criteria and the results that belong to the current implementation. For each criterion, record the specific result that supports it and the scope that result actually exercised; mark a criterion uncovered when no result reaches it. Stop with an acceptance-to-evidence map, without converting uncovered rows into inferred success.

## Anti-pattern

Listing a test suite, build, and manual check as "verification complete" because they all passed, while never showing whether persistence, authorization, or another required outcome was exercised.

## Why

Checks prove only the behavior and state they observe. Mapping them to acceptance exposes silent coverage gaps and prevents a dense verification log from being mistaken for complete capability evidence.

## Exceptions and boundaries

A single result may cover several criteria when its observable scope genuinely includes each one; do not duplicate work just to force one result per row. If acceptance itself is missing or disputed, resolve that authority problem before inventing criteria for this map.

## Example

A form test proves that two fields render, and an integration result proves that saving survives reload. The map marks both criteria covered but leaves "unauthorized users are rejected" uncovered because neither result exercised it.
