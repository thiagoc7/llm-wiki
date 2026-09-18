# Real-world application (anonymized)

This template isn't theoretical — it's the distilled skeleton of vaults I run daily. Below is one anonymized application (a **live decision journal for market research**) to show what the method looks like when it's *operated* for real, with custom tooling built on top.

> Everything here is described at the level of **architecture and patterns**. No real entities, numbers, sources, or credentials.

## The shape

External commentary and my own analysis flow in, get distilled into one note per idea, and every decision (act / watch / skip) is recorded **with its reasoning** — so calls can be reviewed later. Three layers, as in the template: raw captures → curated notes → schema.

## Tooling built on top

The method is just Markdown + conventions. The leverage comes from tools wired around it:

- **Durable, event-driven scheduler/watchdog.** A long-lived process runs routines on time (a pre-session brief, an end-of-day journal, a weekly review) and reacts to events — surviving restarts, never double-firing. The vault is maintained on a heartbeat, not by hand.
- **Data / quote fetcher.** A small stdlib tool pulls fresh numbers from public sources to keep state notes current at ingest time.
- **Commentary ingestion.** External commentary streams are digested incrementally into the `sources/` layer, then distilled into curated notes — "as if I'd read everything and summarized it."
- **Action tool with a hard human gate.** For anything that touches the real world, the tool requires a **dry-run first** and an explicit **human approval step** before it executes. The AI prepares; the human commits. Irreversible actions are never automatic.
- **Multi-agent split.** A lightweight "capture" agent keeps the raw layer current around the clock; a heavier "analyst" agent runs the deep sessions. They coordinate through the append-only `log.md` and the shared schema.

## Human-in-the-loop, by tier

Every routine is tagged with how much autonomy it has:

| Tier | Meaning |
|---|---|
| ✅ AUTO | The AI does it unprompted (refresh state, file a source, update the index). |
| 🟡 SEMI-AUTO | The AI proposes; a one-word confirm runs it. |
| 🔴 ON-REQUEST | Only when explicitly asked. |
| ⚫ MANUAL | Human-only; the AI must never do it (e.g. committing a real-world action). |

That's the whole point: the vault is fast where speed is safe and **stops for a human where it isn't**.

## Why this matters

The generic template shows you *know* the pattern. This shows the difference between knowing it and **operating** it: durable scheduling, real data, a hard approval gate, and a multi-agent division of labor — built and maintained as a living system, not a one-off.
