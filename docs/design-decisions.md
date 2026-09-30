# Design decisions

## Deterministic scoring before AI generation

AI is not used to decide who enters the pipeline. Configurable, inspectable rules
rank prospects consistently and make the recommendation explainable.

## Local generation

A locally hosted model reduces unnecessary external data transfer and lets the
workflow continue without a metered cloud-model dependency.

## Validation after generation

Generated copy is treated as a candidate, not trusted output. Rules check for
unsupported claims, fabricated figures, inappropriate pricing or links, and
incorrect references before the draft reaches an operator.

## Deterministic fallback

Model downtime should not break an operational workflow. A constrained template
provides a predictable fallback that can still be reviewed and edited.

## Draft-only boundary

Gmail integration stops at draft creation. Human approval remains the final
control before any communication is sent.

