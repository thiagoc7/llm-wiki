---
type: experiment
updated: 2026-02-03
status: in_progress
subject: "Campaign X"
change: "Pause the low-performing keyword group on Campaign X."
hypothesis: "The group spends without converting; pausing it frees budget for terms that do convert."
confidence: medium
metrics_before:
  click_through_rate: 0.012      # 1.2% — placeholder, fictional
  cost_per_click: 0.00          # fill with your unit; fictional placeholder
  conversions_30d: 0
metrics_after:
  click_through_rate: null       # fill after the 7-day window
  cost_per_click: null
  conversions_30d: null
becomes_learning: null
tags: [example, fictional, optimization]
---

# Pause keyword group — Campaign X (2026-02-03)

> **Fictional example.** Campaign, metrics, and outcome are invented to
> demonstrate the marketing-ops experiment format. No real account, numbers,
> or spend.

## The change
Paused one underperforming keyword group inside Campaign X. The group has been
accumulating clicks with no conversions over the trailing 30 days. The rest of
the campaign is left untouched so the effect is isolated.

## Hypothesis
The group spends budget without producing conversions. Pausing it should free
that budget to flow to the terms that *do* convert, improving overall
efficiency without losing meaningful volume. Mechanism: budget is shared at the
campaign level, so removing a non-converting drain reallocates spend toward
better terms.

## Result
<!-- Fill in after the 7-day follow-up window. -->
- **Status:** in_progress
- **What the metrics show:** _pending — re-check on 2026-02-10._

## Learning
<!-- If this validates, promote it to a learning note and link it in becomes_learning. -->
_Not yet — awaiting the follow-up window._

## Rollback (if applicable)
Re-enable the paused keyword group on Campaign X. No other settings were
changed, so re-enabling fully reverses the experiment.
