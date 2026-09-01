---
anti_patterns:
  - description: Providing useful considerations and background without an observable action or stopping point, encouraging the reader to keep exploring after enough evidence exists.
    id: pack-creator.authoring.guidance-without-decision
    name: Guidance that never reaches a decision
    severity: warn
applies_when: a Practice trigger is already clear, but its Guidance does not yet tell the reader what to do, what output to produce, and when the decision is complete
id: pack-creator.authoring.write-concrete-guidance-and-stop-condition
severity: warn
stage: authoring
tech_stack:
  - lorelum-pack-authoring
title: Give Concrete Actions and a Clear Stop
---

## When to apply

Apply while writing Guidance for a Practice whose trigger and single decision are already settled.
This Practice controls the action and its stopping point. It does not decide when the Practice
should be retrieved or whether the failure scenario is realistic.

## Guidance

Use concrete verbs that name what to inspect, compare, choose, record, or change. Identify the
minimum facts needed, the output of the decision, and a condition that ends further research or
expansion. Remove advice that cannot change the output. Stop when a reader can follow the Guidance
and show one observable result without inventing an extra workflow.

## Anti-pattern

An operations Pack draws from incidents where emergency failover settings differed across regions.
The author gives a thorough list of resilience principles, topology questions, and possible tools
because flexibility seems safer than prescribing an order. A capable operator can study every item
and still not know which configuration to compare or when the failover review is complete, so
investigation expands while the inconsistent setting remains.

## Why

Guidance changes behavior only when it leads from the trigger to a bounded output. Without a
stopping point, even relevant advice can produce delay, unnecessary scope, or incompatible
interpretations.

## Exceptions and boundaries

Exploratory Practices may end with a bounded evidence gap or an explicit request for a decision
rather than a technical choice. Safety and incident response may require immediate containment
before full analysis. In both cases, name the observable handoff or containment state that ends this
Practice.

## Example

A frontend Pack helps teams keep product colors consistent. For a proposed one-off color, the
Guidance says to inspect the semantic theme tokens and representative call sites, choose an existing
token when its meaning matches, or record the unmet semantic need for a new token. It stops once one
choice and its affected component are named; it does not require cataloging every color in the
application.
