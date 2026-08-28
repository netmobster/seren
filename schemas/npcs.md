<!-- Copyright (c) 2026 Jeremy Wright. All rights reserved. Published for review only; no licence granted. See LICENSE.txt -->

# NPCs — a capture pipeline, not a library

**Revised 2026-08-24.** This directory originally proposed a pre-built NPC
library. That was wrong, and the reasoning is worth keeping.

---

## The reversal

The AI can generate a tavern keeper on demand, easily and well. Generation was
never the problem.

**What it cannot do is generate the *same* tavern keeper in session 9 that it
improvised in session 3.** That is a **persistence** problem, not a generation
problem — and session logs already solve persistence.

A thousand pre-written people is an expensive fix for a problem we don't have.

---

## What we build instead

### 1. Generate in situ

NPCs appear as the plot needs them. No pre-population, no roster to maintain, no
directory of strangers nobody will ever meet.

### 2. Persist on contact

**The moment a player interacts with an NPC, that NPC is written to canon.**
This is the load-bearing mechanic. Everything else is convenience.

Captured on first contact:

```yaml
name:
role:
location:            # bound at capture
first_seen:          # session ref — provenance
stat_block:          # SRD reference, only if combat is plausible
wants:               # ONE line
voice:               # how they actually talk, 1-2 lines
tell:                # a physical habit to hang narration on
knows:               # visibility-tagged — see architecture §3
  - fact:
    visibility:      # true | known | suspected | false
```

`knows` **must** carry visibility, or an NPC cannot hold a secret without the DM
leaking it. See [`../docs/architecture.md`](../docs/architecture.md) §3.

### 3. Promote when remembered

An NPC moves to `named/` the first time the player remembers their name unasked.
That's the moment they stop being furniture and start being a character.

### 4. Seed generation from trait tables — the ONE thing a corpus buys

Improvised NPCs drift toward a single voice. Ask for a blacksmith, then a guard,
then a priest, and eventually the whole world sounds like one person doing
voices.

The fix is **variety at the point of generation**, not coverage in advance.
[mjmcphee/dnd-npc-generator](https://github.com/mjmcphee/dnd-npc-generator) by
Mike McPhee is MIT and genuinely **2024-native** (uses "species", not "race").

⚠️ **Right-sized 2026-08-24:** it is a **small personal project** — 1 star, 1
fork, 4 commits — and its tables are **inline Python dictionaries inside the
script**, not data files. It is a **starting point, not a corpus.** Expect to
extend it heavily, and don't plan around it as though the problem is solved.

See [`../docs/open-source-resources.md`](../docs/open-source-resources.md) §4.

---

## What we DO pre-build

The default is **only what must be mechanically correct** — stat blocks, which
already live in [`../library/`](../library/) as SRD data.

The split is clean:

| | pre-built | generated |
|---|---|---|
| **stat block** — what it does on its turn | ✅ correctness matters | |
| **personality** — what it wants, how it talks | | ✅ variety matters |

Correctness gets retrieved. Character gets invented, then *captured*.

### Two sanctioned exceptions

**Revised 2026-08-24.** Both are pre-built *people*, not stat blocks, and both
earn it for the same reason: **generation cannot produce them at the moment they
are needed.**

| | why it is exempt |
|---|---|
| [`adventurers/`](adventurers/) | Rival parties and hirelings are built like characters rather than like monsters. Six, converted from superseded player sheets. |
| [`antagonists/`](antagonists/) | **A nemesis is defined by recurrence**, and recurrence cannot be improvised — the accumulation has to have been designed before the first meeting. Six, and six is the ceiling. |

Nothing else here is pre-built, and the bar for adding a third exception is the
same test: *does improvising this at the table produce the wrong thing, rather
than merely a different one?*

---

## Structure

```
npcs/
  tables/
    roles/
      town/        20 roles — people who live in a settlement
      world/       12 roles — people who live outside one
      hostile/     10 command-tier roles — droppable threats
    names/ traits/ hooks/    generation seeds  (⬜ unbuilt — VLUM task 2)
  adventurers/     6 rival adventurers, built like characters
  antagonists/     6 recurring nemeses, built like characters
```

⚠️ **Captured NPCs are not stored here.** They live inside the campaign, at
`LIVE/<campaign>/canon/locations/<place>/npcs/`, because **canon is
campaign-bound**. There is no `captured/` and no `named/` directory —
promotion is a `status:` field, so a path never changes. See
[`../docs/npc-containers.md`](../docs/npc-containers.md) §1 and
[`../docs/campaign-start.md`](../docs/campaign-start.md) §1.

---

## Status

| piece | state |
|---|---|
| `tables/roles/` | ✅ **42 built** — 20 town, 12 world, 10 hostile |
| `adventurers/` | ✅ **6 built** |
| `antagonists/` | ✅ **6 built 2026-08-24** |
| `tables/names/ traits/ hooks/` | ⬜ **the remaining gap.** Mechanical, unblocked, no design required. |

The capture pipeline itself depends on the canon store (build step 5).
