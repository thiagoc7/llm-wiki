---
type: concept
updated: 2026-01-15
status: active
tags: [reference]
---

# Glossary

> Shared vocabulary for this vault. Concept notes are durable — edited in place,
> not dated. Keep definitions short and link entities with `[[wikilinks]]`.
>
> _The terms below are generic to the method, plus two fictional examples._

## Vault terms

- **Vault** — a Markdown knowledge base an LLM keeps alive: raw sources →
  curated wiki → schema. See [[CLAUDE]].
- **Source** — a raw, immutable capture in `sources/`. Never edited.
- **Curated note** — a note in `wiki/` / `concepts/` / `state/`, written and
  maintained by the AI from sources.
- **Decision** — a record of a choice and the *reason* behind it. The core
  entity of a decision journal. See [[wiki/decision-journal]].
- **Experiment** — one change + hypothesis + before/after + outcome. See
  [[wiki/marketing-ops]].
- **Learning** — a validated rule distilled from one or more experiments.
- **Ingest** — the workflow that files raw input and updates the curated layer.
  See [[CLAUDE#Ingest]].
- **Lint** — the hygiene workflow that finds broken links, missing frontmatter,
  and orphans. See [[CLAUDE#Lint]].

## Example domain terms (fictional)

- **Advisor A / Advisor B** — placeholder names for external sources that surface
  decision prompts. Use generic labels, never real identities.
- **Example Corp (EXMPL)** — a fictional company used in decision-journal examples.
- **Campaign X** — a fictional marketing campaign used in marketing-ops examples.
