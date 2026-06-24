# CLAUDE.md — Vault Schema & Operating Manual

This file is the **schema**: the operating manual an AI assistant follows to keep this vault alive. It is the third layer of a [Karpathy-style LLM wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) (raw sources → curated wiki → schema). Read this file first, before touching anything.

> This is a **generic template**. Rename the domain folders, redefine the entity types, and adjust the fields below to your use case. Everything here is convention, not law — but the value of the vault comes from following the conventions *consistently*.

## Principles

1. **Three layers, never mixed.** `sources/` is raw and immutable. `wiki/` + `concepts/` + `state/` are curated by the AI. This `CLAUDE.md` is the schema. Don't let raw data leak into curated notes unedited, and don't edit raw sources.
2. **Capture is append-only.** Every ingest adds; it never silently rewrites history. Corrections are new notes or new log lines, not edits to the past.
3. **Reasons over data.** A note's value is the *judgment* it records (the decision, the hypothesis, the "why"), not the raw numbers. Always capture the reasoning.
4. **Compound over time.** Each ingest should make the vault more useful: update the entity, refresh the index, append the log. If an ingest doesn't connect to anything, that's a signal something is missing.
5. **The structure is the memory.** Because conventions are explicit and machine-readable, any session can resume cold. Keep frontmatter, naming, and links disciplined so the next session (human or AI) isn't lost.

## Conventions

### Frontmatter (required on every curated note)

Every note under `wiki/`, `concepts/`, and `state/` starts with YAML frontmatter. The three universal fields:

```yaml
---
type: decision        # the entity type — see "Entity types" below
updated: 2026-01-15   # ISO date of the last meaningful edit (the AI keeps this current)
status: active        # active | watching | resolved | archived | draft
---
```

Each entity type may add its own fields (see the templates in `templates/`). Raw notes in `sources/` carry a *lighter* frontmatter recording provenance only:

```yaml
---
type: source
captured: 2026-01-15
origin: "manual paste"   # where it came from, generically (paste / transcript / export / link)
---
```

### Wikilinks

Link entities with `[[wikilinks]]`, using vault-relative paths so links survive moving files and render in Obsidian-style editors:

- `[[wiki/decision-journal/2026-01-15-advisor-a-example-corp]]` — link to a note
- `[[index]]`, `[[log]]`, `[[CLAUDE]]` — link to the core files
- `[[concepts/glossary#Some term]]` — link to a heading
- `[[wiki/decision-journal/...|Advisor A on Example Corp]]` — link with display text after `|`

When you move or rename a note, update the wikilinks that point to it (a vault-wide search-and-replace) and append a log line noting the move.

### Naming

- **Dated event/decision/experiment notes:** `YYYY-MM-DD-<slug>.md` (e.g. `2026-01-15-advisor-a-example-corp.md`).
- **Entity pages** (a person, company, project — things, not events): `<slug>.md` (e.g. `advisor-a.md`).
- Slugs are lowercase, hyphen-separated, no real-world identifying detail you wouldn't want public.

### Entity types

Define your own. The examples in this template use:

| `type` | Lives in | One note = |
|---|---|---|
| `source` | `sources/` | One raw capture, verbatim |
| `decision` | `wiki/decision-journal/` | One decision + its reason + later outcome |
| `experiment` | `wiki/marketing-ops/` | One change + hypothesis + before/after + outcome |
| `learning` | `wiki/marketing-ops/` | A validated rule distilled from one or more experiments |
| `concept` | `concepts/` | A durable definition, playbook, or rule |
| `state` | `state/` | A current-state snapshot (overwritten, not appended) |

### Index & log discipline

Two files are the spine of the vault. Keeping them current is **not optional** — it's the bookkeeping the AI exists to do.

- **`index.md`** — the live catalog. Lists active entities and notes, grouped by status. The AI updates it on every ingest, decision, and cleanup. It is rewritten freely (it reflects the *present*).
- **`log.md`** — the append-only changelog. Every meaningful action appends one line: `## [YYYY-MM-DD HH:MM] <action> — <summary>`. Never edit past log lines; only append.

## Automation levels

Every action falls into one of four levels. **Respecting these is the core of human-in-the-loop.** Over-automating loses trust; under-automating creates friction. Tune the boundaries to your comfort, but always make the level explicit.

| Level | Symbol | When to run | Examples |
|---|---|---|---|
| **AUTO** | ✅ | Always, no need to ask | Save raw to `sources/`, create/update curated notes, update `index.md` & `log.md`, fix wikilinks, lint |
| **SEMI-AUTO** | 🟡 | Do it, then surface a one-line summary for the human to confirm or correct | Mark a decision `resolved`, conclude an experiment `validated`/`rolled_back`, promote an experiment to a `learning` |
| **ON-REQUEST** | 🔴 | Only when the human explicitly asks | Bulk reorganizations, deleting/archiving notes, rewriting the schema, anything destructive or hard to reverse |
| **MANUAL** | ⚫ | The AI can't or shouldn't do it — tell the human to | Running external tools/integrations, anything requiring credentials, real-world execution outside the vault |

**Rule of thumb:** if it only adds to the vault → ✅ AUTO. If it changes a *judgment* (a status, a conclusion) → 🟡 confirm. If it's destructive or structural → 🔴 ask first. If it leaves the vault → ⚫ hand off to the human.

> **No secrets, ever.** This vault is meant to be shareable. Never write credentials, API keys, tokens, account numbers, or private personal data into any note. If a source contains them, redact before saving to `sources/`.

## Workflows

### Ingest

When the human pastes raw material and says *"ingest this"*:

1. ✅ Save the raw input verbatim to `sources/YYYY-MM-DD-<slug>.md` with provenance frontmatter. **Do not edit the content** — this is the immutable record. Redact only secrets/credentials.
2. ✅ Identify the entities involved (which decision, experiment, person, project, concept). For each, create the curated note from the matching template in `templates/`, or update the existing one.
3. ✅ Fill the note's body from the source, in *your* words where it's a summary, quoting the source where exact wording matters. Link back: the curated note's `## Source` section wikilinks the raw note.
4. ✅ Cross-link related entities with `[[wikilinks]]`.
5. ✅ Update `index.md`: add or move the note under the right status grouping.
6. ✅ Append to `log.md`: `## [YYYY-MM-DD HH:MM] ingest — <what came in>, touched: <notes>`.
7. 🟡 Briefly summarize for the human what you filed and where, and flag anything ambiguous.

### Query

When the human asks a question across the vault:

1. Answer from the **curated layer** (`wiki/`, `concepts/`, `state/`) — that's what it's for.
2. **Cite** the notes you used with `[[wikilinks]]`, so the human can drill in.
3. If a claim is load-bearing, trace it back to its raw source and note that link.
4. If the answer reveals a gap (an entity with no page, a decision with no recorded outcome), say so — and offer to fix it (a 🟡 action).

### Lint

When the human asks you to *lint* the vault (or periodically, as an ✅ AUTO hygiene pass):

1. ✅ **Broken wikilinks** — find `[[...]]` targets that don't resolve to a file/heading. List them; offer to fix.
2. ✅ **Missing frontmatter** — find curated notes missing `type` / `updated` / `status`, or with an unknown `type`.
3. ✅ **Stale `updated`** — find notes whose body clearly changed but whose `updated` date didn't (and vice versa).
4. ✅ **Orphans** — find entities no other note links to, and sources never ingested into a curated note.
5. ✅ **Index drift** — find notes that exist on disk but aren't reflected in `index.md`, or index entries pointing at moved/deleted notes.
6. Report findings as a checklist. Fixing trivial issues (link paths, dates) is ✅ AUTO; anything that changes a judgment or deletes content is 🟡/🔴.

## Quick reference — phrases that trigger action

| You say | The AI does |
|---|---|
| *"ingest this: …"* | Ingest workflow (✅) |
| *"decision: watching/act/skip on X because …"* | Create/update a `decision` note + index + log (✅) |
| *"that experiment validated / roll it back"* | Conclude the experiment, update status (🟡), promote to `learning` if asked |
| *"what do we know about X?"* | Query workflow, with citations |
| *"lint the vault"* | Lint workflow (✅) |
| *"where do things stand?"* | Read/update `state/handoff.md` |
| *"reorganize / delete / archive …"* | ON-REQUEST (🔴) — confirm scope first |
