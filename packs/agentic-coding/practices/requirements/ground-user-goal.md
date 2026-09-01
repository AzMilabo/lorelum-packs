---
anti_patterns:
  - description: The agent adopts a plausible component or work product as the goal because it offers fast visible progress, allowing a polished implementation to miss the result the user actually needs.
    id: agentic-coding.requirements.solution-shaped-goal
    name: Solution-shaped goal
    severity: warn
applies_when: the agent is about to frame or continue work without a current statement of the observable result the affected user or operator needs
id: agentic-coding.requirements.ground-user-goal
severity: warn
stage: requirements
tech_stack:
  - agentic-coding
title: Ground Work in the User Goal
---

## When to apply

Apply at task start, or when implementation details have displaced the reason for the work, if no
current sentence states who needs what result. If the result is clear and only the definition of
done is missing, define acceptance instead.

## Guidance

Read the current request and any accepted issue or specification. Write one sentence naming the
affected person, the result they must observe, and any explicit constraint that changes it.
Components, tests, documents, and abstractions are possible means, not the goal. If two
interpretations produce different outcomes, ask for the decision. Stop when the sentence can reject
work that does not advance the result.

## Anti-pattern

Support staff need to locate delayed orders from a customer reference. Because the repository
already has an attractive operations dashboard, the agent adds a delayed badge there and gets the
component tests green. The dashboard works, but staff still cannot search with the reference
customers provide.

## Why

A concrete outcome gives later decisions a stable comparison point. Without it, repository structure
and visible artifacts can replace user value while superficial checks still pass.

## Exceptions and boundaries

For an exact mechanical request, such as renaming a supplied label, the user's wording may already
be the complete goal. This Practice identifies the result; it does not list acceptance checks or
non-goals.

## Example

A request says to improve failed uploads, and the repository already has a generic error banner that
would make a message-only patch easy. The agent first records: "Creators can identify the failed
file and retry it without re-uploading files that already succeeded." That goal leaves UI design
open and shows why changing only the banner would not solve the request.
