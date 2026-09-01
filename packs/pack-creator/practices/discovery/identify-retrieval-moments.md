---
anti_patterns:
  - description: The author uses policy chapters or repository folders as retrieval moments because they preserve source organization, leaving real decision queries scattered across several topics or unmatched by any Practice.
    id: pack-creator.discovery.source-outline-as-retrieval-map
    name: Source outline used as the retrieval map
    severity: warn
applies_when: the Pack outcome is known and the author is about to select Practices without first identifying the recurring moments when a reader would benefit from the collection
id: pack-creator.discovery.identify-retrieval-moments
severity: warn
stage: discovery
tech_stack:
  - lorelum-pack-authoring
title: Identify When the Pack Should Be Retrieved
---

## When to apply

Apply after the Pack's decision outcome is clear and before turning source material into individual
Practices. Identify the recurring moments when the target reader is about to choose, approve,
diagnose, or report something and timely guidance could change the result. A later authoring
decision writes the trigger for one Practice; this Practice maps collection-level opportunities for
help.

## Guidance

Trace the work in which the target decisions occur and list concrete moments in the form "when the
reader is about to decide or act on X under Y condition." Use observed questions, review comments,
incidents, and near misses to find moments that a source outline may hide. Merge synonyms, remove
moments that do not support the Pack outcome, and note high-consequence gaps. Do not force the list
into one fixed lifecycle. Stop when the map covers the important decisions without prescribing the
exact Practice files that will implement it.

## Anti-pattern

A privacy-compliance Pack should help product teams make correct data-handling choices. The accepted
policy is divided into retention, consent, access, and vendor chapters, so using those headings as
the retrieval map preserves authority and makes provenance easy. Real questions arrive instead while
adding a database field, designing account deletion, or approving an analytics vendor. Each question
crosses several chapters, and queries for those moments retrieve broad policy summaries rather than
a usable decision. The better map starts from those recurring product choices and links the relevant
policy facts afterward.

## Why

Retrieval happens from the reader's current situation, not from the author's source navigation.
Mapping those situations exposes missing help before content is divided into files.

## Exceptions and boundaries

Some Packs support event-driven work, ongoing review, or rare high-risk decisions rather than a
linear workflow. Their moment map should reflect that reality. A source chapter may also be a
genuine retrieval moment, but only when readers actually frame their decision that way. This
Practice does not define one Practice's final trigger wording.

## Example

An on-call operations Pack aims to improve decisions that prevent noisy alerts from becoming missed
incidents. The author identifies three useful moments: before changing an alert threshold, when
repeated alerts have no clear owner, and before closing an incident with muted notifications still
active. These moments guide later Practice discovery. The author does not add a Practice for every
monitoring-tool menu or assume that alert creation, response, and closure must form a universal
workflow.
