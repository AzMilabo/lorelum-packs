---
id: agentic-coding.review.run-subtractive-review-before-commit
title: Run a Subtractive Pre-Commit Review
stage: review
tech_stack:
  - agentic-coding
applies_when: an implementation diff is ready to commit or hand off, and the agent must decide whether every added file, abstraction, fallback, interface, I/O pass, test, and document has a current reason to remain
severity: warn
anti_patterns:
  - id: agentic-coding.review.deletion-as-success
    name: Deletion as success metric
    description: Optimizing the review for fewer lines or files can remove required behavior and protections while making an underbuilt diff appear disciplined.
    severity: warn
---

## When to apply

Apply to the completed diff immediately before it becomes a commit or review handoff, when its additions can be judged together. Do not apply while choosing between designs during implementation, or as a demand to minimize a diff that already contains only justified work.

## Guidance

Inspect each material addition against a current requirement, demonstrated risk, stable contract, or necessary implementation dependency. Remove additions with no present reason, consolidate duplicate logic, and replace local reinventions with already-suitable capability, while retaining behavior and protection that the evidence justifies. Stop with the smallest diff that still satisfies the accepted outcome and its risk boundaries.

## Anti-pattern

Celebrating deletion count, then removing an explicitly required extension point or authorization check because it makes the patch smaller, while leaving an unneeded helper because it looks conventional.

## Why

Implementation accumulates locally reasonable extras that are easier to see as a system at the diff boundary. A subtractive pass reduces unsupported surface and maintenance cost without turning minimality into a substitute for correctness.

## Exceptions and boundaries

Keep apparently unused migration, compatibility, security, audit, or rollback machinery when current contracts or rollout state require it. If simplification would change a public contract or accepted architecture, return that decision to the appropriate authority rather than deleting it during cleanup.

## Example

A pre-commit pass removes a second date-normalization helper and an unused fixture export, reuses the existing parser, and keeps the batch-size guard and recovery marker because the import contract requires both.
