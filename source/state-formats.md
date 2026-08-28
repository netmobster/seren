<!-- Copyright (c) 2026 Jeremy Wright. All rights reserved. Published for review only; no licence granted. See LICENSE.txt -->

# State formats — `LIVE/<campaign>/state/`

**The live game.** Written continuously as things change, not at session close.
See [`../LIVE/README.md`](../LIVE/README.md) §1 for the write cadence.

| file | holds | lifecycle | spec |
|---|---|---|---|
| `ledger.jsonl` | every event that changes state | **never discarded** | §2 ✅ |
| `party.md` | status for the party — PCs and companions | **persists** across scenes and sessions | §3 ✅ |
| `scene.md` | where we are, initiative, foes, beat position | **wiped** when the scene ends | §4 ✅ |
| `queue.md` | NPCs met but not yet written to a container | promoted at session close | ⬜ |
| **`facts.jsonl`** | **every change to what is TRUE and who KNOWS it** | **never discarded** | **§5 ✅** |

> ### ⚠️ This file is operational, not rationale
>
> **It can be handed to a session that has read nothing else.** Why these
> formats exist lives in [`architecture.md`](architecture.md); **what they are
> lives here.** Keep it that way.

---

# 1. The status block

**Every creature in play has the same status shape.** A player character, a
DM-run companion and `wolf-2` all carry an identical block. What differs is
**lifecycle, not shape** — PCs persist, foes evaporate when the fight ends.

That is why the reconstruction in §2.5 is *one* procedure rather than two, and
why a foe who survives and starts recurring can be promoted into the party layer
without changing anything about how their state is written. Same discipline as
[`npc-containers.md`](npc-containers.md) §7: **promotion is a field, not a path.**

```yaml
<slug>:
  hp:            {current: 62, max: 79, temp: 0}
  conditions:    []
  concentration: {spell: null, since_round: null}
  slots:         {1: 4, 2: 3, 3: 3, 4: 3, 5: 2, 6: 1}   # omit if none
  uses:          {arcane_recovery: 1, fey_step: 4}       # omit if none
  death_saves:   {successes: 0, failures: 0}             # omit until relevant
  exhaustion:    0
  hit_dice:      {remaining: 11, die: d6}
```

| field | | |
|---|---|---|
| `hp` | always | **`temp` does not stack** — a new grant replaces the old only if higher. |
| `conditions` | always | list of `{cond, src, until}`. `until` in `actor:when` form so expiry is derivable rather than remembered. |
| `concentration` | casters | `since_round` is what makes duration checkable. |
| `slots` · `uses` | if they have them | `uses` keys match `resources` on the character sheet exactly. |
| `death_saves` | ⚠️ PCs | **Required the moment a PC reaches 0 HP.** Foes usually just die. |
| `exhaustion` | always | ⚠️ **Its own field, not a condition.** 2024 exhaustion *stacks*, reduces every D20 test by `2 × level`, and **level 6 is death**. |
| `hit_dice` | always | short rests spend them. |

**Slug convention.** PCs use the filename slug from `characters/`
*(`jornis-the-forgotten`)*. Foes use a slug plus an index whenever there is more
than one — `wolf-1`, `wolf-2` — because *"the wolf took 8"* is unreconstructable
with three wolves on the board.

---

# 2. `ledger.jsonl` — the event ledger

**One JSON object per line. Append-only. Written the moment the event happens.
Never edited, never reordered, never discarded.**

> ## The one rule
>
> ### An entry records what HAPPENED. It never records what a resource is AT.
>
> `"roll": 8` ✅ — that is what the dice said.
> `"hp_after": 44` ⛔ — that is a conclusion, and it does not belong here.
>
> **Nothing in this file states a current total.** Not HP, not slots remaining,
> not uses left. Those live in §1's status blocks and are *derived* from this
> file plus the character sheet.

**Adjudications ARE recorded** — `hit`, `pass`, `crit`. Those are decisions, not
totals.

---

## 2.1 The envelope

```json
{"id":"e014","rd":3,"t":"attack","...":"type-specific fields"}
```

| field | | |
|---|---|---|
| `id` | **required** | `e` + sequence, in file order. Stable, never reused. The handle other entries reference. |
| `rd` | **required in combat** | round number. `null` outside initiative. |
| `t` | **required** | entry type. |
| `ref` | optional | `id` of the entry that caused this one. Links damage to its attack, a save to the spell that forced it. |
| `note` | optional | short free text — the DM's own adjudication reasoning. *Why* this DC, *why* advantage. |

## 2.2 Every type has a declared shape

**The vocabulary is open; the shapes are not.** New types are created by using
them — same extension model as module `elements/` — but **a new type declares its
required and optional fields here before its first use.** A type used twice
without a declared shape is a bug in this file, not a judgement call.

Each type below lists **required** fields and *optional* ones. The envelope
fields in §2.1 apply to all of them and are not repeated.

---

## 2.3 Roll types

```json
{"id":"e007","rd":2,"t":"attack","src":"wolf-1","tgt":"jornis-the-forgotten","roll":17,"mods":[["prof",4],["str",3]],"total":24,"vs":17,"crit":false,"hit":true}
{"id":"e008","rd":2,"t":"damage","ref":"e007","src":"wolf-1","tgt":"jornis-the-forgotten","dice":"2d6+3","roll":8,"mods":[["heavy_armor_master",-3]],"total":8,"dtype":"piercing"}
{"id":"e009","rd":2,"t":"save","ref":"e008","who":"jornis-the-forgotten","kind":"con","dc":10,"roll":12,"mods":[["con",3]],"total":15,"pass":true,"for":"concentration"}
{"id":"e010","rd":2,"t":"check","who":"jornis-the-forgotten","skill":"arcana","dc":15,"roll":9,"mods":[["int",5],["exp",8]],"total":22,"pass":true}
{"id":"e001","rd":1,"t":"init","who":"jornis-the-forgotten","roll":11,"mods":[["dex",2]],"total":13}
{"id":"e031","rd":9,"t":"death_save","who":"jornis-the-forgotten","roll":4,"result":"fail"}
{"id":"e041","rd":null,"t":"hit_dice","who":"jornis-the-forgotten","dice":"1d6+3","roll":7}
```

| type | required | optional |
|---|---|---|
| `attack` | `src` `tgt` `roll` `total` `vs` `hit` | `mods` `crit` |
| `damage` | `dice` `roll` `total` `dtype` `tgt` ⚠️ | `src` `mods` `crit` |
| `save` | `who` `kind` `dc` `roll` `total` `pass` | `mods` `for` |
| `check` | `who` `dc` `roll` `total` `pass` | `skill` *or* `ability`, `mods` |
| `init` | `who` `roll` `total` | `mods` |
| `death_save` | `who` `roll` `result` | — |
| **`death_fail`** | `who` `n` `why` | `ref` |
| `hit_dice` | `who` `dice` `roll` | — |

**`roll` is always the raw die**, before anything is added. `total` is what it
came to. **`mods` is a list of `[name, value]` pairs, and it is optional** — but
when present, `total` should equal `roll` plus the mods.

> ### ⚠️ `total` is REQUIRED on `damage`, and this is the field most often got wrong
>
> **`roll` is the dice and nothing else. `total` is the damage dealt.** Every
> roll type carries both — `damage` is not an exception, and treating it as one
> is the single most common way this file gets written incorrectly.
>
> **The worked example above, step by step:**
>
> | | |
> |---|---|
> | `dice: "2d6+3"`, `roll: 8` | the two dice came up 8. **Not 11 — the `+3` is not part of the roll** |
> | the `+3` in the expression | 8 + 3 = 11 |
> | `mods: [["heavy_armor_master", -3]]` | 11 − 3 = 8 |
> | **`total: 8`** | **the damage actually dealt** |
>
> ⭐ **`roll` and `total` being equal here is a coincidence** of this example, and
> a deliberate one — if you can read this entry correctly you can read any of
> them.
>
> **The check, and it needs no knowledge of the game:**
> `total == roll + (the modifier inside dice) + (the sum of mods)`.
> **If that does not hold, the entry is wrong.** So is any `roll` outside the raw
> range of `dice` — a `1d10+4` cannot roll 12.

⚠️ **`tgt` is required on `damage` UNLESS the damage is an area effect**, in
which case it is omitted and per-target outcome comes from the `save` entries
that `ref` it. **Blanket-optional was wrong** *(corrected 2026-08-26)*: a
single-target hit with no `tgt` forces the reconstruction in §2.5 to walk back
through `ref` to the `attack` to find out whose HP to subtract from, and an
entry that cannot say who it happened to is not a record of what happened.

**Resistance and vulnerability are never applied here**; they are derived from the sheet at reconstruction. `mods` on damage is
for riders that are *not* derivable from a stat block alone — Empowered
Evocation's `+5`, Heavy Armor Master's `−3`.

`death_save` `result` ∈ `success` · `fail` · `crit_success` *(nat 20 — regain
1 HP)* · `crit_fail` *(nat 1 — counts as two failures)*.

⭐ **`death_fail` records failures caused by DAMAGE rather than by a roll.**
Taking damage at 0 HP costs a failure and a critical hit costs two, and **no die
is thrown for either** — so they cannot be written as `death_save`, whose shape
requires a `roll`. Without this type the failure count is unrecoverable at
reconstruction.

`n` is 1 or 2. `why` ∈ `damage` · `crit_damage_at_0`. `ref` points at the
`damage` entry that caused it.

```json
{"id":"e094","rd":9,"t":"death_fail","who":"jornis-the-forgotten","n":2,"why":"crit_damage_at_0","ref":"e093"}
```

*Declared in play by the third probe run, using §2.2's own extension rule, and
adopted here unchanged.*

---

## 2.4 State-event types

**This is the half a roll log cannot hold, and the reason this file is a
ledger.** Spending a spell slot involves no die. Neither does dropping
concentration by casting a second spell, a condition expiring, or drinking a
potion.

```json
{"id":"e005","rd":1,"t":"cast","who":"jornis-the-forgotten","spell":"moonbeam","slot":2,"conc":true}
{"id":"e006","rd":1,"t":"use","who":"jornis-the-forgotten","feature":"fey_step"}
{"id":"e044","rd":null,"t":"recover","who":"jornis-the-forgotten","feature":"arcane_recovery","slots":{"3":1,"2":1,"1":1}}
{"id":"e012","rd":3,"t":"cond","who":"wolf-1","cond":"prone","op":"start","src":"topple","until":"self:end_next_turn"}
{"id":"e020","rd":5,"t":"conc","ref":"e019","who":"jornis-the-forgotten","op":"end","spell":"moonbeam","why":"new_spell"}
{"id":"e024","rd":6,"t":"heal","who":"jornis-the-forgotten","dice":"2d4+2","roll":9,"src":"potion_of_healing"}
{"id":"e002","rd":null,"t":"temp_hp","who":"seren","amount":11,"src":"wild_shape"}
{"id":"e040","rd":null,"t":"rest","kind":"short"}
{"id":"e050","rd":7,"t":"down","who":"wolf-2","why":"damage"}
```

| type | required | optional |
|---|---|---|
| `cast` | `who` `spell` `slot` | `conc` |
| `use` | `who` `feature` | `n` *(defaults to 1)* |
| **`recover`** | `who` `feature` | `slots` `uses` |
| `cond` | `who` `cond` `op` | `src` `until` |
| `conc` | `who` `op` | `spell` `why` |
| `heal` | `who` `roll` *or* `amount` | `dice` `src` |
| `temp_hp` | `who` `amount` *or* `dice`+`roll` | `src` |
| `rest` | `kind` | — |
| `down` | `who` `why` | — |

**`cast` is what spends a slot** — there is no separate "slot spent" event.
`slot: 0` means a cantrip.

⭐ **`recover` is what puts resources back when a rest doesn't.** Arcane Recovery
restores slots totalling half the wizard's level **and the player chooses
which** — that choice is real information and it is unreconstructable if it
isn't written down. `slots` is a map of level → count; `uses` is the same for
features. Without this entry, slot state stops being derivable the moment the
feature is used, which is exactly when a long fight needs it most.

`conc.why` ∈ `damage` · `new_spell` · `incapacitated` · `voluntary` · `ended`.
⚠️ **A failed concentration save does not end concentration by itself** — the
`save` entry records the roll, this entry records the consequence. **Both are
written.**

`down` marks a creature reaching 0 HP. Cheap, and without it every subsequent
round's silence from that creature is unexplainable.

`rest.kind` ∈ `short` · `long`. What it restores is derived from the sheet.

---

## 2.5 Reconstruction

**Given this file and the character sheets, current state must be derivable
without reading a single line of narration.**

1. Start from the sheets — max HP, full slots, full uses, no conditions.
2. Walk the ledger in `id` order.
3. Apply each entry **using the rules**, never using anything the entry concluded
   about totals. `damage` → subtract, after applying resistance from the sheet.
   `cast` → decrement that slot. `recover` → add back exactly what it names.
   `rest` → restore per the rules.

**If step 3 needs information that is not in the ledger and not on a sheet, the
schema has a hole.** Write it down rather than inferring it from the transcript.

---

# 3. `party.md` — the persistent side

**YAML frontmatter is the machine layer; prose below is for humans.**

**One file for the whole party**, characters as top-level keys, each carrying a
§1 status block. One character or four — mechanically identical.

```yaml
---
round_synced: 3          # last ledger round applied — makes staleness visible
jornis-the-forgotten:
  hp:            {current: 62, max: 79, temp: 0}
  conditions:    []
  concentration: {spell: moonbeam, since_round: 1}
  slots:         {1: 4, 2: 2, 3: 3, 4: 3, 5: 2, 6: 1}
  uses:          {arcane_recovery: 1, fey_step: 3}
  death_saves:   {successes: 0, failures: 0}
  exhaustion:    0
  hit_dice:      {remaining: 11, die: d6}
---

Anything a person needs that YAML shouldn't carry.
```

**`round_synced` is the one field that isn't in the status block.** It records
which ledger round this file has been brought up to date with. Without it, a
stale file and a correct file look identical.

---

# 4. `scene.md` — the transient side

**Everything true about *right now*.** Wiped and rewritten when the scene
changes, which is what makes it the correct home for foes.

Four things live here.

```yaml
---
where:    "the mill loft, after dark"
present:  [jornis-the-forgotten, wolf-1, wolf-2, wolf-3]
round:    3
initiative:
  - {who: wolf-1, total: 15}
  - {who: jornis-the-forgotten, total: 13}
  - {who: wolf-2, total: 11}
foes:
  wolf-1:
    hp:         {current: 4, max: 11, temp: 0}
    conditions: [{cond: prone, src: topple, until: "self:end_next_turn"}]
    exhaustion: 0
    hit_dice:   {remaining: 2, die: d8}
beats:
  - {beat: the-sheep-finds-them,  status: done,    session: S01}
  - {beat: nokes-agents-arrive,   status: done,    session: S01}
  - {beat: shinebright-explains,  status: next}
  - {beat: the-approach,          status: skipped}
  - {beat: noke-confronted,       status: blocked, by: shinebright-explains}
---

Zones, described. Free text — see below.
```

**`foes` carries the same §1 status block as `party.md`.** Identical shape,
different lifecycle. A foe who survives and starts recurring gets promoted to an
antagonist and their block moves; nothing about how it is written changes.

**`beats` records position in the module's beat graph.** `status` ∈ `done` ·
`next` · `blocked` · `skipped`. **`skipped` is deliberately distinct from
not-yet** — a beat that was cut is a different fact from one still ahead, and the
module's `load_bearing: no` beats exist to be cut.

## 4.1 Zones are free text, and soft rules apply

**No enum, no coordinates.** Theatre of the mind — architecture §7. The entire
positional vocabulary is narrative: *in melee · at range · behind the pillar ·
up the tree.* An enum would be the first step back toward a grid.

**But free text is not free of consequence.** Position is fiction, and fiction
has to stay coherent:

> If the player has established that they are **hiding up a tree**, and then
> declares they attack the monster fighting the party **in the tavern** — that is
> clearly not one turn. *(Jay, 2026-08-26.)*

The DM adjudicates distance and reachability from what has been described, and
**holds it consistently**. That is a contract obligation rather than a state
one — architecture §7 flags the same problem for positional abilities like
Sculpt Spells, emanations and polearm reach.

---

# 5. `facts.jsonl` — the knowledge ledger

**`ledger.jsonl` records what HAPPENED. This records what is TRUE and who knows
it.** Append-only, written **immediately**, never discarded.

> ## ⭐ Why it exists as a file rather than as context
>
> **The module schema's `reveals:` declares visibility transitions** — a twist
> is a fact moving `true → known`. **Nothing on disk received them.**
>
> ⛔ **So mid-session, every flip lived only in the model's context** — which
> is exactly the window where leaking matters. Session two then began from a
> canon file written by the same model summarising what it *thought* it had
> revealed. **The fog-of-war contract had no memory.**

---

## 5.1 The four visibility values

**Same vocabulary as the module schema's cast `knows:` and its `reveals:`
blocks** — not a second mechanism.

| value | the world | the party |
|---|---|---|
| **`true`** | it is so | **has not learned it** |
| **`known`** | it is so | **knows it** |
| **`suspected`** | it is so | **suspects, has not confirmed** |
| **`false`** | it is **not** so | **believes it anyway** |

⭐ **`false` is the one the whole design exists to keep.** A party that is
confidently wrong is the most playable state in the game, and it is
unrecoverable if nobody wrote it down.

## 5.2 The envelope

```json
{"id":"f003","s":2,"op":"flip","...":"op-specific fields"}
```

| field | | |
|---|---|---|
| `id` | **required** | `f` + sequence, in file order. Stable, never reused |
| `s` | **required** | **session number.** ⭐ The close ceremony promotes everything since the last close, and without this it cannot tell what is new |
| `op` | **required** | `flip` · `establish` · `believe` |
| `beat` | optional | the module beat this came from, if any |
| `note` | optional | short free text — the DM's reasoning |

⚠️ **`s` has no equivalent in `ledger.jsonl`, which also spans sessions.**
That is a real gap in §2.1 and it is **not** fixed here — flagged rather than
silently patched, because changing the ledger envelope invalidates 313 entries
of regression data.

## 5.3 The three operations

```json
{"id":"f001","s":1,"op":"flip","fact":"The sheep is a wizard, not a beast.","from":"true","to":"known","beat":"the-sheep-finds-them"}
{"id":"f002","s":1,"op":"establish","fact":"The innkeeper's son runs errands for Noke.","visibility":"true","src":"play"}
{"id":"f003","s":2,"op":"believe","fact":"Noke is dead.","truth":"false","note":"party assumed after the collapse; he fled through the cellar"}
{"id":"f004","s":2,"op":"flip","fact":"The guards are transmuted people.","from":"suspected","to":"known","how":"Guz said it outright"}
```

| op | required | optional | |
|---|---|---|---|
| **`flip`** | `fact` `from` `to` | `beat` `how` | **an existing statement changes visibility** |
| **`establish`** | `fact` `visibility` | `src` | **a new statement enters the record** — including ones no module contained |
| **`believe`** | `fact` `truth` | `note` | ⭐ **the party has concluded something, and `truth` says whether they are right** |

**`from` and `to` are two of the four §5.1 values.** ⚠️ **A `flip` whose `from`
never appeared in an earlier `establish` or in the module is a bug** — something
changed visibility that was never true in the first place.

**`src` ∈ `module` · `play` · `player`.** ⭐ **`player` is legitimate** —
architecture's *nobody is punished for creativity*, and a player who invents a
detail the DM adopts has established a fact.

> ### ⭐ `believe` with `truth: false` is the entry that earns this file
>
> **`flip` and `establish` describe the world. `believe` describes the party**,
> and it is the only one of the three that records something the DM must then
> **play against**.
>
> ⚠️ **It is also the one that will get skipped**, because a false belief
> forms quietly and nothing prompts you to write it down. **If this file has no
> `believe` entries after three sessions, that is the finding.**

## 5.4 What does NOT go here

| | |
|---|---|
| ⛔ **The fact's content, in full** | `fact` is one sentence. **The prose belongs in `canon/`** |
| ⛔ **NPC state** | a person met but unwritten goes to `queue.md`, then a container |
| ⛔ **Anything with a die roll** | that is `ledger.jsonl`. **A perception check is a roll; what it revealed is a flip. Both are written** |

## 5.5 ⛔ It has no consumer yet

> ### **`facts.jsonl` works for session one and silently rots from session two.**

**Nothing promotes it into `canon/`.** The session-close ceremony that would —
**SRN-34** — is unbuilt, so entries accumulate and are never consolidated.

⚠️ **This is a dependency, not a nice-to-have**, and it was missed by two
separate red-team passes. **Writing the file is correct and sufficient for the
build-test**, which only checks that it exists and is empty at t=0. ⛔ **It is
not sufficient for play.**

*(Same disease this repo has now named four times: **anything that happens at a
moment needs a named dispatcher, or it does not happen.**)*
