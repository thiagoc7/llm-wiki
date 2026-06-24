---
type: decision
updated:                 # ISO date, kept current by the AI
status: watching         # active | watching | resolved | archived
prompt_by:               # who/what surfaced this (e.g. "Advisor A", "self") — generic, no real names
subject:                 # the thing being decided about (e.g. "Example Corp")
decision: watching       # act | watching | skip
reason:                  # one line: WHY this decision
trigger:                 # what would change the decision (the condition you're waiting on)
outcome: open            # open | good-call | bad-call | n/a  (filled in on review)
tags: []
---

# {{Subject}} — {{decision}} ({{date}})

## The prompt (what surfaced this)
<!-- What was flagged, and by whom. 2–3 sentences. Keep names generic. -->

## The decision
- **Decision:** {{act | watching | skip}}
- **Reason:** <!-- the WHY — this is the most valuable line in the note -->
- **What would change it:** <!-- the trigger / invalidation condition -->

## Source
- **Prompted by:** <!-- e.g. Advisor A (generic) -->
- **Raw note:** [[sources/...]]

## Review (fill in later)
<!-- When the situation resolves, judge the decision. Was it a good call, regardless of how it turned out? -->
- **What happened:**
- **Was the decision good?** good-call | bad-call | n/a
- **What I learned:**
