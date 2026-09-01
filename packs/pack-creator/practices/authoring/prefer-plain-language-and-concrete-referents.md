---
anti_patterns:
  - description: Preserving source jargon because it sounds authoritative, even though readers and translators cannot map the words to one observable action or object.
    id: pack-creator.authoring.abstract-language-as-precision
    name: Abstract language mistaken for precision
    severity: warn
applies_when: a Practice uses abstract nouns, compressed jargon, or coined terms where the author could name the actual person, artifact, action, or observable state
id: pack-creator.authoring.prefer-plain-language-and-concrete-referents
severity: warn
stage: authoring
tech_stack:
  - lorelum-pack-authoring
title: Use Plain Words for Concrete Things
---

## When to apply

Apply during sentence-level review when a cold reader may not know what an abstract term refers to.
This Practice controls wording. It does not decide whether the Why section contains the right causal
reason or whether an Example includes enough scenario facts.

## Guidance

Underline nouns and verbs that could refer to several things. Replace them with the actual actor,
artifact, action, or observable state. When a technical term is necessary, define its concrete
referent on first use and then use it consistently. Prefer one ordinary sentence over a coined label
plus explanation. Stop when a reader and translator can point to what changes without inventing a
local definition.

## Anti-pattern

An operations Pack turns incident guidance into "operationalize the observability posture through
telemetry harmonization." The phrase resembles the policy source and therefore feels precise and
defensible. But it does not say whether the engineer should align field names, sampling rates, alert
thresholds, or dashboards, so different readers and translations produce different actions while
preserving the same impressive words.

## Why

Concrete language ties guidance to an observable decision. Abstract language hides competing
interpretations, which weakens both retrieval matching and human review across languages.

## Exceptions and boundaries

Keep standard domain terms when practitioners use them consistently and the distinction matters.
Legal or regulatory wording may need to remain exact, but explain the operational object or action
it governs. Do not replace precise technical language with a longer but equally vague paraphrase.

## Example

A compliance Pack helps reviewers decide whether an exception is auditable. Its source requires the
request, approver, and governing policy version to be recorded. Instead of "retain sufficient
exception provenance," the author writes, "Record who requested and approved the exception and which
policy version allowed it." Each referent is reviewable, and no new compliance rule was invented.
