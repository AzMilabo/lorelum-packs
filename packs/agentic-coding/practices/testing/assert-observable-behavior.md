---
id: agentic-coding.testing.assert-observable-behavior
title: Assert Observable or Stable Behavior
stage: testing
tech_stack:
  - agentic-coding
applies_when: >-
  a test's protected behavior is already known, and the agent is about to
  choose assertions that could observe either a user-visible or stable
  interface outcome or incidental implementation structure
severity: warn
anti_patterns:
  - id: agentic-coding.testing.incidental-implementation-assertion
    name: Incidental implementation assertion
    description: Asserting private state, call order, markup shape, or helper boundaries that are not contractual, which makes harmless refactoring look like behavioral regression.
    severity: warn
---

## When to apply

Apply when writing or revising the assertion for a behavior whose purpose is already established. Prefer what a user, caller, downstream system, or stable interface can observe. The near miss is deciding which requirement deserves coverage; that is a test-purpose decision, not an assertion-shape decision.

## Guidance

Identify the observer named by the protected behavior and the stable outcome available to that observer. Assert that outcome at the narrowest reliable boundary, supplying controlled inputs and observing outputs or effects rather than reconstructing private execution. The output is the observable assertion. If only internal details are currently visible, create or use the smallest legitimate observation seam instead of declaring an incidental detail to be the contract.

## Anti-pattern

Checking component state names, exact internal call sequences, incidental markup nesting, or temporary helper invocations when the actual requirement concerns saved data, returned results, permissions, or other externally meaningful effects.

## Why

Observable assertions fail when promised behavior changes, while implementation assertions also fail when behavior is preserved through refactoring. Testing the stable boundary therefore protects outcomes with less false coupling and produces evidence that maps more directly to acceptance.

## Exceptions and boundaries

Exact bytes, syntax trees, protocol fields, event order, timing bounds, or serialization shape should be asserted when those details are themselves published or safety-relevant contracts. Focused unit tests may observe an internal API that is intentionally stable within the project. Do not weaken precision when precision is part of the requirement.

## Example

For a profile update, the test submits a new display name and verifies that a subsequent read returns it. It does not assert the component’s internal state variable or the order of two private helper calls.
