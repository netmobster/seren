<!-- Copyright (c) 2026 Jeremy Wright. All rights reserved. Published for review only; no licence granted. See LICENSE.txt -->

# Modules — the portable adventure format

**v0.1, written 2026-08-25. Deliberately thin.**

> ⚠️ **This spec has never been run.** It is written to be rewritten by the first
> build-test. Do not polish it — the misfits found converting a real adventure
> are the actual specification, and a beautiful schema authored ahead of contact
> is wrong in expensive ways.

---

## What a module is

**A module is to a campaign what a gear is to an operator.** The same file for
every Seren user; what each person *does* with it differs entirely.

```
campaigns/modules/<slug>/     the module      · TEMPLATE · portable · may ship
LIVE/<campaign>/              the playthrough · INSTANCE · yours    · never ships
```

`campaign-start.md` is the function between them. The module is its input.

### It is structure and direction, never prose

**The module gives the DM something to point at. The DM owns the world.**

| the module owns | the DM owns |
|---|---|
| what is true · what is in motion · what must happen · the numbers · who is named | the village, the weather, every word anyone says, when and how anything lands |

That is [architecture §0](../../docs/architecture.md)'s **EXACT / INFERENCE**
split, one altitude up.

> ### ⛔ Never transcribe the source
>
> No boxed read-aloud, no encounter prose, no lifted description. **Write our own
> summary of what is true.**
>
> This is not only a licensing rule. **Boxed prose hands the model a script where
> it needs a situation** — the railroading failure mode in
> [architecture §6](../../docs/architecture.md). A module built from someone
> else's adventure and a module we wrote from scratch look the same, because the
> thin version is the correct version either way.

---

## Structure

```
campaigns/modules/<slug>/
  module.md         frontmatter + premise + beats + cast + fronts + scaling
  elements/         typed blocks — one file each, see §4
  README.md         only if the module needs one
```

---

## 1. Frontmatter

```yaml
module:        a-wild-sheep-chase
version:       "0.1"
title:         "A Wild Sheep Chase"
author:        "R.M. Jansen-Parkes — Winghorn Press"

ruleset:       dnd-2024           # ⭐ which rules this module is written against
derivation:    derived            # original | derived
derived_from:  "A Wild Sheep Chase (2016)"
licence:       "DMs Guild Community Content Agreement"
shareable:     no                 # follows derivation — see campaigns/README.md

native_level:  "4-5"              # what it was WRITTEN and playtested at
party_size:    "4-5"              # matters as much as level, and nobody records it
sessions:      1
tone:          comic              # feeds DM-persona.md at session zero
```

### `ruleset:` — added 2026-08-25, and it is future-proofing

**Points at `library/<ruleset>/`.** Today there is exactly one — `dnd-2024` — so
it is a constant. **The field exists so that a second one costs a rename rather
than a migration.**

**Why it is worth a line now:** an audit of what in Seren is actually D&D-bound
found that **the narrative layer is entirely portable** — beats, cast, elements,
fronts, the visibility contract and the container spec contain no dice at all.
The mechanics are isolated in `library/` and `characters/`. A module that
declares its ruleset is the join between the two.
See [`../../labs/ruleset-portability.md`](../../labs/ruleset-portability.md).

⚠️ **Two other fields quietly assume D&D**, and are left as-is deliberately:

| field | assumption |
|---|---|
| `native_level` | that **levels exist**. A levelless system has nothing to put here — *Cairn was rejected for exactly that reason.* |
| `party_size` | that a party is a D&D-shaped party. |

**Not fixed today.** Both are load-bearing for the only ruleset that exists, and
generalising them before a second one exists would be designing against an
imaginary requirement. **Recorded so the next person does not think it was
missed.**

**`shareable` is not a formality.** A derived module is someone else's work in a
new wrapper. `derivation: derived` implies `shareable: no` and the two should
never disagree.

**`native_level` is what the module IS.** What *this run* is doing lives in
`LIVE/<campaign>/campaign.md`. Template says what it is; instance says what we
are doing with it.

---

## 2. Beats — what must happen, never how

**The load-bearing idea, and the one the project did not have.**

[Architecture §6](../../docs/architecture.md) says *write agendas, never plot* —
fronts and clocks. **That is correct for open campaign play and wrong for an
authored adventure.** A one-shot has a designed shape, and replacing it with
fronts destroys the thing that made it worth running.

So there are two tools and a module may carry both:

| | |
|---|---|
| **front** | what moves **whether or not** the party engages |
| **beat** | what must **happen** for the story to complete |

**The metaphor is a screenwriter's beat sheet** *(Jay, 2026-08-25)*: these things
need to occur, but **how, when, and how they are played is the DM's**.

```yaml
- beat: the-sheep-finds-them
  must:  "The party is approached by a sheep that turns out to be a
          transformed wizard asking for help."
  load_bearing: yes
  after:  []
  before: [noke's-agents-arrive]
  reveals:
    - fact: "The sheep is a wizard, not a beast."
      from: true
      to:   known
  dm_owns: "Where they are, what they were doing, how the sheep behaves,
            whether the moment plays funny or unsettling, how long it takes."
```

### The four rules

1. **`must` is a state change, never a scene.** *"The party learns X"*, not
   *"the party is in a tavern when X."* If it reads like a scene, it is too
   specific.
2. **`dm_owns` is mandatory.** Naming what is free per beat is what stops the
   list becoming a script. It is the EXACT/INFERENCE line drawn beat by beat.
3. **Order without schedule.** `before` / `after` are *soft* constraints, not a
   sequence. Sheep Chase says it outright: *don't force the story back towards
   the ideal path.* A module whose beats only work in one order is a script.
4. **`load_bearing: no` means skippable**, and plenty should be. If every beat is
   load-bearing there is exactly one way through.

### Twists are beats with a visibility flip

**`reveals` interlocks with the fog-of-war contract that already exists**
([architecture §3](../../docs/architecture.md)) instead of inventing a second
mechanism. A twist is a fact moving `true → known`, or `false → known` when the
party has been wrong.

That also means **the DM knows the twist from the start and must not leak it** —
which is precisely what the visibility tags are for.

---

## 3. Cast

**Only what is named and native.** Everything else the world needs is generated
on contact from [`npcs/tables/roles/`](../../npcs/tables/roles/) — 42 templates
covering town, world and hostile. **A module never ships a guard**, because no
adventure ships a guard.

```yaml
- name:       Guz
  native:     yes                 # invented by this module
  stat_block: module              # module | srd:<name> | roles/hostile/<slug>
  want:       "One line."
  voice:      "One or two lines. Ours, not the source's."
  tell:       "A physical habit to hang narration on."
  knows:
    - fact: "…"
      visibility: true | known | suspected | false
```

**Antagonists are not cast.** The standing six in
[`npcs/antagonists/`](../../npcs/antagonists/) are systems the campaign
activates, not module content. If a module has a genuinely native recurring
nemesis, write it as an antagonist and reference it.

⚠️ **A figure whose death ends the plot is a front, not an antagonist** — and in
a one-shot that is usually the villain. Give them a front, or a beat, or both.

---

## 4. Elements — the extension point

**Adopted from Jay, 2026-08-25.** Rather than enumerating every structure an
adventure might contain, modules carry **typed blocks in a common envelope.**
When the next adventure has a chase system, a downtime track or a faction
reputation clock, it slots in **without a schema change.**

`elements/<slug>.md`

```yaml
---
name:
type:          item | consequence | mechanic | location | hazard | …
summary:       one line
description:   what it is, in the world
function:      what it DOES — mechanically or narratively
rules:         how it resolves. DCs, damage, saves.
constraints:   what it cannot do. The guard rails.
---

## Content
The big blob. Everything that did not fit above.
```

**`type` is open.** New types are created by using them; the envelope is the
contract, not the vocabulary.

Two types worth naming because both already turned up in one adventure:

- **`item`** — the custom magic item. *(WotC-era module convention, per Jay: a
  bespoke item was more or less expected.)*
- **`consequence`** — the branch outcomes. An adventure with four endings has
  four of these, and none of them are beats, because **they record what becomes
  true afterward rather than what must happen.**

---

## 5. Scaling — `rescale(module, level)`

**Exactly symmetric with `devolve(master, level)`, including where it fails.**

| | derivable | **must be authored** |
|---|---|---|
| character | features, ASIs, slots, subclass | **equipment** |
| module | encounter budget, XP thresholds, treasure values | **premise integrity** |

```yaml
scaling:
  down: "What to cut. Which encounters collapse into one."
  up:   "What to add. Where the pressure has to come from instead."
  breaks_at: |
    ⚠️ REQUIRED. What makes the premise stop working.
    Not encounter balance — no CR table catches this.
```

**`breaks_at` is the field that earns this section.** Sheep Chase is the worked
example: upvolve it far enough and a party with a high-slot `Dispel Magic` simply
un-sheeps the wizard in scene one and the adventure evaporates. That is the
module equivalent of handing a level 5 character a Rod of the Pact Keeper +2 —
and [architecture §2b](../../docs/architecture.md) already says the engine should
**refuse** in that situation.

**A rescale that has not answered *"can the party now bypass this in one
action?"* is not finished.**

---

## 6. DM persona seed

**Added 2026-08-25 (Jay).** `tone:` in the frontmatter was carrying this on its
own and could not.

**The module knows what register it needs.** An adventure whose whole value is
comic timing, or dread, or procedural grind, is telling you how it wants to be
run — and losing that between the module and the table is how a good adventure
becomes a pleasant, forgettable one.

But `DM-persona.md` is **instance layer**. It is *who is running this game*,
settled at session zero, and swappable. So the same split as everything else:

> **The module proposes. Session zero disposes.**

```yaml
dm_persona_seed:
  register:   "The voice this module needs, in a sentence."
  lethality:  "What this adventure assumes about death, and whether it telegraphs."
  pacing:     "How long a scene runs before something happens."
  lean_into:  "What to push. The thing that makes this module work."
  avoid:      "The specific way a DM ruins this one."
  tells:      "What this DM is harsher about, and what it finds funny."
```

> ### ⛔ THESE SIX FIELDS ARE v1 AND THE PERSONA FORMAT IS v2 — SRN-37
>
> ⚠️ **Four of the seven dials in
> [`../../dm/persona-format.md`](../../dm/persona-format.md) have no field here**
> — roll frequency, failure texture, canon generation, callback appetite.
> **The Registrar came back from the v2 retrofit with all four marked
> `unset — no source`**, which is how this was proven rather than suspected.
>
> ⭐ **So a module cannot currently propose the dial that most changes how the
> game feels.** And `lethality` proposes a setting **a persona may no longer
> hold** — it moved to `dm/table-agreement.md` §3 with the rest of the player's
> standing position.
>
> **Until this is fixed, `campaign-start.md` §2 asks for the missing four
> directly.**

**It is a seed, not a profile.** campaign-start hands it to session zero as a
recommendation the player can overrule — the same *recommend, then confirm*
pattern as the equipment and spell passes in
[`campaign-start.md`](../../docs/campaign-start.md) §4.

**`avoid` is the field that earns this section.** Every module has one specific
way a well-meaning DM kills it, and it is almost never obvious from the text.

---

## 7. The fill list

**The amendment shopping list**, borrowed from the gear pattern: the module
**declares its own extension points** rather than leaving campaign-start to
guess.

```yaml
fill_at_campaign_start:
  - what: "Which town this opens in"
    why:  "The module needs a settlement; it does not care which"
  - what: "Party level and size"
    why:  "native 4-5; see scaling"
  - what: "Which of the six antagonists are activated"
    why:  "None are native to this module"
  - what: "Transposition of the custom item"
    why:  "Gear transposes, never imports — architecture §2b"
```

Anything the module leaves `null` should appear here. **A null with no fill-list
entry is a bug**, not a blank.

---

## 8. When not to use · negative parameters

**Also from the gear pattern — every gear says what it is not.** A bare
adventure conversion drops this, and it is the part that prevents a module being
run in a situation it cannot survive.

- **Party sizes it breaks at.** ⚠️ Seren runs one PC plus 2–3 DM-run
  companions. That is *similar headcount, very different action economy* to four
  independent players, and it is more likely to need retuning than level is.
- **What it cannot absorb** — tone, content, a party that solves it sideways.
- **Its failure mode.** The way this module goes wrong when it goes wrong.

---

## 9. Provenance

Where it came from, what was read, what was authored, what was deliberately left
unnamed for the campaign to fill. Same discipline as every other file here.

---

## Status

⬜ **No module has been built.** The first is *A Wild Sheep Chase*, and building
it **is the build-test** — see [`../../docs/pieces.md`](../../docs/pieces.md).

**Every place the adventure does not fit this spec is a finding.** Every slot
that stays empty is either a bad slot or a real question. Both are the output.
