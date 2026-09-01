---
anti_patterns:
  - description: Explaining a rule with broad ideals or remote business value because they sound important, while omitting the immediate mechanism that makes the action necessary.
    id: pack-creator.authoring.distant-rationale
    name: Distant benefit used as the rationale
    severity: warn
applies_when: a Practice has an action but its Why section does not yet explain the direct engineering or decision consequence of following or ignoring that action
id: pack-creator.authoring.explain-the-direct-causal-reason
severity: warn
stage: authoring
tech_stack:
  - lorelum-pack-authoring
title: Explain the Immediate Cause and Effect
---

## When to apply

Apply while writing or reviewing the Why section. The reader already knows the action; the missing
decision is which direct consequence justifies it. This Practice controls causal explanation, not
the wording of every section or the completeness of the Example.

## Guidance

Name the action or omission, the first important system or decision effect it causes, and why that
effect changes the outcome. Prefer a short causal chain that the scenario or source can support.
Remove mission statements and benefits that would be true of almost any good Practice. Stop when the
reader can use the reason to recognize a near miss or justified exception.

## Anti-pattern

A database Pack requires large indexes to be built with an online method. The source records show
that blocking index creation held write locks and delayed orders. Because the Pack supports a
high-level reliability program, the author writes only that "reliable data platforms protect
customer trust and business continuity." The statement is true and persuasive, but it does not
explain the lock mechanism, so readers cannot tell why this index operation differs from a harmless
metadata change.

## Why

The immediate cause lets readers transfer a rule to new situations and identify when its conditions
are absent. A distant benefit may motivate agreement but cannot guide the technical decision.

## Exceptions and boundaries

Some policy rules are justified by an external obligation rather than a technical mechanism. Name
the controlling obligation and the direct compliance consequence instead of inventing engineering
causality. Do not extend the chain beyond what the source supports.

## Example

A security Pack says to verify a token's audience before accepting it. Its Why states: "Audience
verification prevents a token issued for another service from being accepted by this service." That
direct effect explains both the action and its security boundary; a generic claim that validation
"improves trust" would not.
