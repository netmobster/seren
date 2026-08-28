<!-- Copyright (c) 2026 Jeremy Wright. All rights reserved. Published for review only; no licence granted. See LICENSE.txt -->

# LIVE

**The instance layer.** Everything `campaign-start.md` generates, plus everything
play produces. Spec'd 2026-08-25.

> ## The one rule
>
> **Nothing in LIVE is a template, and nothing in LIVE ever ships.**

That is the whole reason it sits at the root rather than inside `campaigns/`.
Every other directory in Seren holds portable material — masters, role
templates, item shapes, antagonists, modules. **LIVE holds one person's actual
game.** One directory, one rule, and the public/private boundary stops being a
judgement call.

```
campaigns/modules/<slug>/     the module    · template · portable · may ship
LIVE/<campaign>/              the playthrough · instance · yours  · never ships
```

Same split as `characters/` vs `builds/`, and as top-level `canon/` vs campaign
canon. This is that distinction applied at the top.

---

## 1. The write cadence — corrected 2026-08-25

**[architecture.md](../docs/architecture.md) §5 said state is ephemeral and
nothing is written until session close. That was wrong**, and it was wrong in a
way that would have broken the thing Seren exists to fix.

> **If a player talks to an NPC and then walks away for three weeks, that
> interaction has to survive.** A session that ends by being abandoned is the
> normal case, not the exception — and "written at session close" loses
> everything when there is no close.

The fix is that §5 conflated two different writes:

| | what | when |
|---|---|---|
| **local write** | LIVE — containers, interaction logs, scene, HP, the roll log | **continuously, as it happens** |
| **true-up** | the durable record — session log, summary, canon promotions, deltas that outlive a long rest | **at session close** |

**SelfActual vault principle #7 — *write at completion, not real time* — governs
the second, not the first.** It is a rule about what the pod receives, and LIVE
is not the pod. It is local working state. The pod, the repo, or wherever the
durable record lives still only ever sees finalised state.

**This is the same shape as Imprint's good-night ceremony.** Work accumulates
locally all session; the close is when it gets reconciled, summarised and
pushed. Nothing is lost in between because the local write already happened.

### What that means in practice

- An NPC container is written **on contact**, not at close.
- An interaction log gets its line **when the exchange ends**, not at close.
- HP, slots and conditions are written **as they change**.
- The **roll log** appends **every roll, immediately** — that is the only thing
  that makes softening detectable after the fact.
- Session close **reconciles**: writes the log and summary, promotes canon,
  advances clocks, and trues up whatever durable store we are using.

**Crash safety is a side effect and a real one.** A closed laptop mid-dungeon
costs nothing.

---

## 2. Structure

See [`_SAMPLE/`](_SAMPLE/) — a folder that documents itself. It contains the
directory shape and READMEs explaining what lands where, and **no campaign
data**, because generating that is `campaign-start`'s job and not something to
hand-author into a sample.

```
LIVE/<campaign>/
  campaign.md          this table's run — tone, session zero, what got activated
  DM-persona.md        WHO is running it
  fronts.md            what is in motion
  ideas.md             what could be wired in, untriggered
  builds/              the party, devolved to this campaign's level
  canon/
    locations/         state.md · charactermap.md · npcs/ — filled ON CONTACT
    antagonists/       interaction logs for activated nemeses
    characters/        per-PC secrets, campaign-specific
  state/               THE LIVE GAME — see §3
  sessions/            session logs, written at close
```

---

## 3. `state/` — the part that has never existed

Everything above is *authored* or *accreted*. `state/` is **the live game**, and
it is where several pieces specified elsewhere in Seren have had no home:

| file | what | written |
|---|---|---|
| `party.md` | current HP, temp HP, slots, conditions, concentration, uses-per-rest | as it changes |
| `scene.md` | where we are, who is present, what is happening, round + initiative if in combat | as it changes |
| `queue.md` | NPCs met but not yet written to a container — the capture queue from [`npc-containers.md`](../docs/npc-containers.md) §7 | on contact |
| `ledger.jsonl` | every roll: what, DC, result, outcome — [architecture §1](../docs/architecture.md) | **immediately, always** |

> ### ⭐ Formats now specified — [`../docs/state-formats.md`](../docs/state-formats.md)
>
> **Added 2026-08-26.** All three live formats are written. Two things this table did not previously say:
>
> - **`scene.md` also holds FOE STATE and BEAT POSITION.** Monster hit points had no home anywhere in this spec — a real gap, since a fight cannot be reconstructed without knowing when something dropped. They live in `scene.md` because that is the file with the matching lifecycle: **PCs persist, foes evaporate when the scene ends.**
> - **Every creature carries the SAME status block** — PC, companion or `wolf-2`. Lifecycle differs; shape does not. That is why a foe who starts recurring can be promoted without changing how their state is written, exactly as [`npc-containers.md`](../docs/npc-containers.md) §7 promotes by field rather than by path.

**`state/` is scratch and is meant to be.** Session close promotes what matters
out of it and it can be discarded. Everything else in LIVE is durable.

**`ledger.jsonl` is the exception — it is never discarded.** It is the only
defence against the DM quietly softening results, and its whole value is
being long enough to show a pattern.

---

## 4. Secrets — two kinds, only one lives here

Easy to get wrong, and getting it wrong moves files that should not move.

| | lives | why |
|---|---|---|
| `npcs/antagonists/<slug>-secrets.md` | **stays put** | declares the *forks* — decisions a campaign must make. Portable, no campaign specifics. |
| `LIVE/<campaign>/canon/…/secrets.md` | **here** | the *answers* — which fork was chosen, what is true in this game |

Same pattern as `grudge:`. **The template asks the question; LIVE holds the
answer.**

---

## 5. Naming

`LIVE/<campaign-name>/` — one directory per playthrough, named for the campaign
rather than the module, because the same module can be run more than once and
those are different games.

**[`_SAMPLE/`](_SAMPLE/) is not a campaign** and never becomes one. It is the
structure, documented, and it is the thing to copy from.
