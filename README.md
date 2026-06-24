# Vault Template — a Karpathy-style LLM wiki

A clonable, generic template for building a **"vault"**: a Markdown knowledge base that an LLM keeps alive for you. You feed in raw material; the AI does the bookkeeping — curating notes, maintaining an index, wikilinking entities, and appending a chronological log — so the knowledge base *compounds* over time instead of rotting.

This is the open-source skeleton of the method. It ships with **no real data** — every example is obviously fictional. Clone it, delete the examples, point your AI assistant at `CLAUDE.md`, and start ingesting.

> **Credit & inspiration.** The pattern is popularized by Andrej Karpathy's note on using an LLM to maintain a personal wiki:
> <https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f>
> This template turns that idea into a reusable, conventions-first repo.

---

## What it is

A vault is three layers that you **never mix**:

```
            ┌───────────────────────────────────────────────────────────┐
  LAYER 1   │  sources/      RAW, IMMUTABLE. Exactly what came in.       │
  (raw)     │                Pasted notes, transcripts, exports, links.  │
            │                The AI reads these but NEVER edits them.    │
            └───────────────────────────────────────────────────────────┘
                                      │  ingest
                                      ▼
            ┌───────────────────────────────────────────────────────────┐
  LAYER 2   │  wiki/         CURATED. One page per entity/idea/event.    │
  (wiki)    │  concepts/     Written and maintained BY the AI from       │
            │  state/        sources. Wikilinked. This is the product.   │
            └───────────────────────────────────────────────────────────┘
                                      │  governed by
                                      ▼
            ┌───────────────────────────────────────────────────────────┐
  LAYER 3   │  CLAUDE.md     SCHEMA / OPERATING MANUAL. Conventions,     │
  (schema)  │  templates/    frontmatter, automation levels, workflows.  │
            │                The rules the AI follows. Rarely changes.   │
            └───────────────────────────────────────────────────────────┘
```

- **Layer 1 — raw sources** (`sources/`): append-only, immutable. Whatever you captured, stored verbatim with a little frontmatter (where it came from, when). If you ever need ground truth, it's here.
- **Layer 2 — the curated wiki** (`wiki/`, `concepts/`, `state/`): the living knowledge base. One note per entity, idea, decision, or event. Cross-linked with `[[wikilinks]]`. Written and kept up to date by the AI.
- **Layer 3 — the schema** (`CLAUDE.md` + `templates/`): the operating manual. It tells the AI *how* to ingest, *where* things go, *what* frontmatter to use, and *when* it may act on its own versus when it must ask you first.

## Why it works

- **The AI does the bookkeeping.** The reason knowledge bases rot is that maintaining them is tedious: filing notes, updating the index, fixing links, keeping a changelog. An LLM is *good* at exactly this drudgery. You think; it files.
- **Compounding, not collecting.** Each ingest makes the vault more valuable: a new source updates the relevant entity page, adds an index entry, and appends one line to the log. It's a journal that gets smarter, not a folder that gets fuller.
- **Conventions over cleverness.** Because the schema is explicit and machine-readable (frontmatter, fixed folders, naming rules), any LLM session can pick up where the last one left off. The structure *is* the memory.
- **Auditable.** Raw sources are immutable, the log is append-only, and every curated claim can point back to its source. You can always reconstruct *why* a note says what it says.
- **Human-in-the-loop by design.** The schema marks which actions are automatic and which need your confirmation, so the AI never quietly does something irreversible.

## How to use

1. **Clone & strip.** Copy this repo, delete the example notes under `wiki/`, and clear `index.md` / `log.md` back to their headers. Keep `CLAUDE.md`, `templates/`, and the empty folder structure.
2. **Adapt the schema.** Edit `CLAUDE.md`: rename the domain folders, define your entity types, and adjust the frontmatter fields and automation levels to your workflow.
3. **Point your assistant at it.** Open the vault with an AI coding/notes assistant that reads a project instruction file (this template uses `CLAUDE.md`). The schema is the first thing it should read.
4. **Ingest.** Paste raw material and say *"ingest this."* The AI saves the raw copy to `sources/`, creates/updates the relevant curated notes, refreshes `index.md`, and appends to `log.md`.
5. **Query.** Ask questions across the vault (*"what did Advisor A say about Example Corp?"*, *"show me every experiment we rolled back"*). The AI answers from the curated layer and links back to sources.
6. **Lint.** Periodically ask the AI to *lint* the vault: find broken wikilinks, notes missing required frontmatter, and orphaned entities. (See the `lint` workflow in `CLAUDE.md`.)
7. **Render (optional).** The vault is plain Markdown with `[[wikilinks]]`, so it opens cleanly in [Obsidian](https://obsidian.md/) or any wiki-aware Markdown editor — but it's just files; no app is required.

## Example domains

The template ships with two tiny, fully fictional example domains under `wiki/` to show the method in two very different shapes. **None of the data is real** — names, companies, and numbers are invented placeholders.

### 1. Decision journal (`wiki/decision-journal/`)

A log of *decisions* and the *reasons* behind them — the classic high-value vault. Each entry records a prompt (something an external "Advisor A" / "Advisor B" flagged, or your own idea), the decision you made (act / watch / skip), and *why* — so that later you can review whether the call was good. The value isn't the data; it's the disciplined record of judgment over time.

> Example entry: *"Advisor A flagged Example Corp (EXMPL). Decision: **watching** — thesis is plausible but the entry trigger hasn't fired. Reason: ..."* (`wiki/decision-journal/2026-01-15-advisor-a-example-corp.md`)

### 2. Marketing ops (`wiki/marketing-ops/`)

A different shape: an experiment log for an ops/optimization workflow. Each note is one change with a hypothesis, a before/after metric placeholder, and an outcome (validated / rolled back / inconclusive). Successful experiments graduate into reusable **learnings**.

> Example entry: *"Experiment: pause low-performing keyword group on Campaign X. Hypothesis: frees budget for converting terms. Status: in_progress."* (`wiki/marketing-ops/2026-02-03-pause-keyword-group-experiment.md`)

You can keep one domain, both, or replace them entirely. The point is the *structure*, not the topic.

## Folder structure

```
llm-wiki/
├── README.md                  # this file
├── LICENSE                    # MIT
├── CLAUDE.md                  # ← THE SCHEMA: conventions + automation levels + workflows
├── index.md                   # catalog of the vault (entities, active notes) — kept current by the AI
├── log.md                     # append-only chronological changelog
│
├── sources/                   # LAYER 1 — raw, immutable. Never edited by the AI.
│   ├── .keep
│   └── 2026-01-15-advisor-a-note.md      # example raw capture (fictional)
│
├── wiki/                      # LAYER 2 — curated notes, one per entity/idea/event
│   ├── decision-journal/      #   example domain A: decisions + reasons
│   │   └── 2026-01-15-advisor-a-example-corp.md
│   └── marketing-ops/         #   example domain B: experiments + learnings
│       └── 2026-02-03-pause-keyword-group-experiment.md
│
├── concepts/                  # LAYER 2 — durable knowledge: glossary, playbooks, rules
│   ├── .keep
│   └── glossary.md            # example concept note (fictional)
│
├── state/                     # LAYER 2 — current-state snapshots (overwritten, not appended)
│   ├── .keep
│   └── handoff.md             # "where things stand right now" for the next session
│
└── templates/                 # LAYER 3 — note templates the AI fills in
    ├── decision.md
    └── experiment.md
```

> Swap `wiki/decision-journal/` and `wiki/marketing-ops/` for your own domain folders. Add entity folders (e.g. `wiki/people/`, `wiki/projects/`) as your vault grows — the conventions in `CLAUDE.md` apply uniformly.

## License

MIT — see [LICENSE](LICENSE). Use it, fork it, build your own vault.
