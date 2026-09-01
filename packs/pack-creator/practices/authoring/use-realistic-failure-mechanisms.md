---
anti_patterns:
  - description: Choosing a toy or plainly negligent failure because it is easy to explain, even though it teaches nothing to a capable reader facing a reasonable competing incentive.
    id: pack-creator.authoring.incompetent-straw-man
    name: Obvious mistake used as proof
    severity: warn
applies_when: an anti-pattern is being drafted and the author must decide whether its mistake, incentive, and consequence form a credible recurring failure
id: pack-creator.authoring.use-realistic-failure-mechanisms
severity: warn
stage: authoring
tech_stack:
  - lorelum-pack-authoring
title: Use a Mistake a Capable Practitioner Could Make
---

## When to apply

Apply when selecting or reviewing the failure mechanism for an Anti-pattern. Ask whether a capable
Pack user could make the wrong choice while responding to real pressure or repository evidence. This
Practice judges credibility; a separate review decides whether the scenario includes enough
background to understand it.

## Guidance

Start from an observed incident, a documented near miss, or a faithful composite. Name the locally
attractive choice, the evidence or incentive supporting it, and the worse result that survives
superficial review. Preserve that causal mechanism when details must be anonymized. Reject scenarios
that require ignoring an explicit rule or making a beginner-level mistake. Stop when a reviewer can
explain why a competent person might choose the wrong path and how the Practice changes that
decision.

## Anti-pattern

A compliance Pack should help engineers implement record-retention policy. Its source material
describes a purge job that also deleted records under legal hold because both shared a storage path.
To keep the Practice short, the author instead depicts a careless developer who ignores retention
policy and never deletes anything. The simplified failure is easy to condemn, but it removes the
attractive reuse decision and no longer prepares a capable engineer for the observed risk.

## Why

A credible incentive distinguishes useful guidance from common sense. It lets the reader recognize
the wrong choice before clean code, familiar patterns, or passing focused checks make that choice
look safe.

## Exceptions and boundaries

Foundational Packs may address novice mistakes, but the scenario still needs a believable cause and
a decision the guidance can change. Do not invent dramatic consequences unsupported by the sources.
When no recurring or plausible failure exists, reconsider whether the Practice adds discriminating
knowledge.

## Example

A frontend Pack draws on accessibility bugs in a component library. A link-styled button already
matches the requested visual and is faster to reuse, so an engineer uses it for navigation. Keyboard
behavior and open-in-new-tab semantics then fail despite a clean visual review. The author preserves
that incentive and consequence, making the failure more useful than "the engineer forgot
accessibility."
