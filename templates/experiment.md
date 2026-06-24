---
type: experiment
updated:                 # ISO date, kept current by the AI
status: in_progress      # in_progress | validated | rolled_back | inconclusive
subject:                 # what this experiment touches (e.g. "Campaign X")
change:                  # one line: the change being made
hypothesis:              # what you expect to happen and why
confidence: medium       # low | medium | high
metrics_before:          # placeholder fields — use whatever metrics fit your domain
  metric_a:
  metric_b:
metrics_after:           # fill in after the follow-up window
  metric_a:
  metric_b:
becomes_learning:        # link to a learning note if this graduates into a rule
tags: []
---

# {{Change}} — {{Subject}} ({{date}})

## The change
<!-- Exactly what was done. Be specific enough to reproduce or reverse. -->

## Hypothesis
<!-- What you expect to happen, and why. State the mechanism, not just the outcome. -->

## Result
<!-- Fill in after the follow-up window. Did the hypothesis hold? Any surprises? -->
- **Status:** in_progress
- **What the metrics show:**

## Learning
<!-- If this graduated into a reusable rule, link it. If not, say why (noise, too few data, contradiction). -->

## Rollback (if applicable)
<!-- Exactly how to reverse the change, if needed. -->
