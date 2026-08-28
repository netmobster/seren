<!-- Copyright (c) 2026 Jeremy Wright. All rights reserved. Published for review only; no licence granted. See LICENSE.txt -->

# Library — retrievable rules reference

Rules the DM **looks up** rather than recalls.

> ## ⭐ THE SRD IS PORTED — 2026-08-27
>
> **[`srd-5.2/articles/`](srd-5.2/articles/) — 588 articles, one file per
> thing.** 301 spells · 229 magic items · 41 tagged rules · 17 feats, with
> `index.json` and schemas in
> [`srd-5.2/articles/README.md`](srd-5.2/articles/README.md).
>
> **Class progression for all twelve classes:** [`2024/core.md`](2024/core.md).
>
> ⚠️ **Still out:** mundane equipment, backgrounds, untagged glossary terms.

> ### ⚠️ The note this replaces was wrong, and it is worth saying how
>
> **Rescoped 2026-08-24:** *"This directory was specified as 'port the SRD' —
> chunked spells, chunked monsters, items, tables. **That job is much smaller
> than it looked**, and most of it is already done elsewhere."*
>
> ⛔ **It was not smaller.** It was 588 articles and three separate extraction
> faults, each of which produced output that **looked complete** — a rarity
> value missing from an enum dropped seven magic items including Spell Scroll,
> a wrapped parenthetical dropped six feats, and `pdftotext -layout` dropped
> table cells.
>
> ⭐ **The estimate was made by looking at the dump and judging it sufficient.
> Nobody tried to use it for anything until SRD-10 needed a slot table**, and
> that is when the holes appeared. **A corpus is not verified by being present.**

---

## ⭐ Species and content the SRD does not contain — ruled 2026-08-27

**SRD 5.2 has a limited species list.** ⛔ **Aasimar is not in it**, and two of
the first play-test party are Aasimar.

> ### The master sheet is the source of record, and traits scale by proficiency bonus.

**Where two or more sheets independently assert the same trait, that agreement
is the evidence.** Ser'en and Korth both carry **Darkvision 60**, **necrotic and
radiant Resistance**, and **Healing Hands**.

⭐ **And the sheets encode the scaling without stating it:** Healing Hands is
**4d4 at proficiency bonus 4**, so it is **2d4 at PB 2**. **The rule was
derivable from the data all along.**

⚠️ **This is the point of this directory, applied to itself.** The alternative
was serving the traits from training — **which is exactly the failure the
section below describes**, and it would have been unverifiable.

**Found by the first play-test session, before a die was rolled.** *(Jay took
this option over re-speciesing the characters or dictating traits by hand.)*

⛔ **What this does NOT license:** inventing a trait no sheet asserts. **If the
sheets are silent, ask the player.** ⬜ *Celestial Revelation is believed to
arrive at level 3 rather than 1, and nothing in this repo can confirm it — that
one is flagged, not ruled.*

---

## Why this exists at all

The model has **far more 2014 content in its training than 2024**, and left to
recall rules from memory it will serve 2014 rulings fluently — which is worse
than serving them badly, because fluent wrong doesn't announce itself.

Live examples, all present in our own roster:

| | 2014 | 2024 |
|---|---|---|
| terminology | "race" | **species** |
| inspiration | Inspiration | **Heroic Inspiration** |
| social checks | ad hoc | **Influence** action |
| unarmed strike | attack only | **Damage / Grapple / Shove** choice |
| grapple & shove | contested check | **saving throw** |
| weapon properties | — | **Weapon Mastery** — Vex, Nick, Sap, Slow, Topple, Cleave |
| Wild Shape | forms by CR, stat replacement | uses per level, temp HP |

Underneath the same thesis as the rest of the architecture: **the model is
handed facts, it does not supply them.** Rules are another kind of state.

---

## The distinction that sets the scope

**Not all drift matters equally, and the difference is who can see it.**

### World-side drift is functionally invisible

A 2014 goblin and a 2024 goblin differ by a couple of hit points and some
ability wording. **The player never sees a stat block** — they see "it lunges at
you." You could run 2014 monsters indefinitely and nobody at the table would
know.

### Character-side drift is fatal

**The player is reading their own sheet.** If the DM runs Wild Shape as
2/short-rest with CR caps while Ser'en's file says otherwise, the DM is
contradicting the player's own document. That isn't a rules quibble — it's the
moment the player stops trusting the system.

### And character-side is already solved

**The 14 files in [`../characters/`](../characters/) ARE the retrieval layer for
character rules.** Every feature is written out with its 2024 uses, recharges
and semantics — that's what the 2026-08-24 JSON audit produced. The player's
sheet and the DM's reference are **the same document**, so drift cannot occur
there structurally.

**That removes the largest chunk of what this directory was going to hold.**

---

## Scope — what actually needs building

| piece | status | why |
|---|---|---|
| **`2024/core.md`** — the digest | ⬜ **the real job** | Shared rules the DM adjudicates that no character sheet carries. See below. |
| **Monsters** | ⬜ import from SRD 5.2 | Data, not authoring. And drift-immune per above. |
| **Character rules** | ✅ **done** | Lives in `characters/`. Do not duplicate it here. |
| **Spells** | ⬜ minimal | PC spells are on PC sheets; monster spells arrive with the monster. Only DM-improvised casting is left, and that's small. |
| **Magic items** | ⬜ minimal | SRD items on demand. Homebrew shapes are in [`homebrew-items/`](homebrew-items/). |
| **Improv tables** | ⬜ | Encounters, weather, rumours. Nice to have, blocks nothing. |
| **2014 partition** | ❌ **dropped** | We run 2024 only. A parallel 2014 tree is exactly the hazard this directory exists to prevent, and nothing needs it. |

---

## `2024/core.md` — the digest spec

**Six to ten pages. Not a system port.** The test for inclusion is one question:

> **Does the DM adjudicate this, and is it absent from every character sheet?**

If a character sheet carries it, it's already retrievable. If the player never
sees it, drift doesn't matter. What's left is the middle:

| section | why it's in |
|---|---|
| **Conditions** | Highest-traffic lookup in the game. Short, and constantly wrong from memory. |
| **Action economy** | Action / Bonus Action / Reaction / Free, and what 2024 changed. |
| **Weapon Mastery** | ⭐ **The single most important entry.** Vex, Nick, Sap, Slow, Topple, Cleave, Graze, Push. **New in 2024** — a DM defaulting to 2014 won't know it exists, and half this roster is built around it. |
| **Grapple & Shove** | Now a **saving throw**, not a contested check. Constant, visible, and the player will notice. |
| **Unarmed Strike** | Damage / Grapple / Shove as a choice. |
| **Rests** | Short and long rest rules, and what recovers on which. |
| **Spell preparation** | 2024 changed how preparation and swapping work. |
| **Death saves & dying** | Rare, high-stakes, must be exactly right the first time. |
| **The Influence action** | New in 2024, and it's how social encounters resolve. |

**Explicitly out of scope:** class features, subclass features, species traits,
spell descriptions, individual magic items. All of those are either on a
character sheet or retrieved as data.

### We are allowed to copy this

**SRD 5.2 is CC-BY 4.0 and irrevocable** — released 22 April 2025, including
2025 Monster Manual stat blocks, weapon mastery and crafting.

**This is the one corpus in the entire project we may legally reproduce**, with
attribution. The digest is therefore an **extraction job, not a writing job** —
pull the relevant sections, attribute properly, done.

> ⚠️ **Unverified:** SRD 5.2 reportedly excludes some content — Artificer,
> Beholder, and **Aasimar**. Aasimar matters here because **Ser'en and Korth are
> both Aasimar.** Not confirmed from a primary source; **check the SRD document
> itself** rather than commentary about it. Survivable either way — their traits
> are already written into their character files — but it constrains anything
> Seren ever ships.

---

## Version discipline

**Every file carries its version in frontmatter.** Retrieval must never return a
2014 passage into a 2024 ruling invisibly.

```yaml
---
ruleset: "2024"
source: "SRD 5.2"
license: "CC-BY-4.0"
---
```

**And homebrew is partitioned, not mixed.** [`homebrew-feats/`](homebrew-feats/)
and [`homebrew-items/`](homebrew-items/) are **inspiration, retrieved as
shapes** — never as truth. SRD is truth. Keep the line or the whole retrieval
guarantee is worthless.

---

## Status

⬜ **Nothing acquired yet**, and it blocks nothing — this can happen in parallel
with any other work.

The job is now: **extract one digest, import monsters once.** Not port a system.
