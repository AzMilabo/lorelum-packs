---
anti_patterns:
  - description: The agent treats the source that is newest, most detailed, or easiest to implement as authoritative without checking its status, turning stale behavior or an unconfirmed interpretation into a requirement.
    id: agentic-coding.requirements.promote-convenient-source
    name: Convenient source promotion
    severity: warn
applies_when: current instructions, an accepted specification, code, tests, summaries, or prior decisions disagree, and one of them is about to define intended behavior
id: agentic-coding.requirements.resolve-source-authority
severity: warn
stage: requirements
tech_stack:
  - agentic-coding
title: Resolve Authority Across Conflicting Sources
---

## When to apply

Apply when two or more sources imply different intended behavior and the next decision needs one
baseline. Sources include the current request, an accepted issue or specification, a decision
record, code and tests, and conversation summaries. If they agree and the question is reuse, inspect
the implementation instead.

## Guidance

Isolate the disputed behavior. For each source, state whether it defines what should happen, only
shows what exists now, is an unconfirmed interpretation, or has been replaced. Choose the
controlling source from explicit adoption, an authorized correction, and the repository's stated
rules; detail and recency alone are not enough. Record what controls the behavior and what the other
sources still prove. If no rule resolves a material choice, ask the user or responsible maintainer
before coding it.

## Anti-pattern

An older cleanup job and its green tests delete audit records after one year. A compact session
summary repeats that behavior, so retaining it seems safer than reopening the design. The adopted
retention policy requires seven years, however, and the implementation evidence cannot override it.

## Why

Code, tests, and summaries describe a state; they do not automatically authorize it. Separating
authority from observation prevents convenient existing behavior from becoming the target.

## Exceptions and boundaries

A safety or data-protection rule may override a product instruction when governing policy explicitly
grants that precedence. Record the scope of the override. This Practice chooses which source defines
intent, not the implementation design.

## Example

The accepted migration plan says existing customer identifiers must remain stable, while the current
prototype and its tests generate replacements. Keeping the tested prototype would be cheaper, but
the agent records the plan as authority and the prototype as unfinished state. It does not preserve
replacement identifiers unless that behavior is separately approved.
