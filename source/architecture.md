<!-- Copyright (c) 2026 Jeremy Wright. All rights reserved. Published for review only; no licence granted. See LICENSE.txt -->

# Seren — architecture

The technical spine. **Write this before the DM contract**, because the DM
contract's job is mostly *"here is the state, here are your constraints on it"*
— and you can't write that well before the state schema exists.

---

## 0. The one principle

> ## **EXACT / MECHANICS** vs **INFERENCE / STORY**

Everything below is this line drawn at a different altitude. It is one rule, not
five, and `DM.md` should encode it once:

| altitude | exact / mechanics | inference / story |
|---|---|---|
| **state** (§1) | code owns HP, slots, conditions | model owns what they *feel* like |
| **dice** (§1) | RNG owns the number | model owns what the number *means* |
| **outcome** (§1) | success/failure cannot move | consequence, cost and colour are wide open |
| **rules** (`library/`) | retrieved, version-pinned | applied with judgement |
| **canon** (§3) | what is *true* is fixed | what is *suspected* is fair game |
| **maps** (§7) | no grid, no coordinates | described position, player-fog reference image |

**The model never decides what is true. It decides what everything means.**

That is also the answer to the failure mode on both sides: a model given
authority over the exact layer confabulates; a model denied authority over the
inference layer becomes a rules engine that types prose. Both are fatal, and the
second is the easier one to build by accident while fixing the first.

*Assume this holds permanently. Nothing here is scaffolding.*

---

## 1. The inversion

**The LLM must not own the rules or the dice.**

Every previous AI DM — AI Dungeon onward — failed the same way: they optimised
**narration** and neglected **state**. The model writes gorgeous prose and then
forgets you burned your last 4th-level slot two turns ago.

```
   code  ->  owns HP, slots, conditions, initiative, uses-per-rest,
             concentration, position, time, inventory
   RNG   ->  owns every die roll
   model ->  owns narration, NPC voice, adjudication proposals
             (never storage, never the dice)
```

The model is **told** the state each turn. It never stores it. If the model
rolls, it fudges toward narrative satisfaction — that is what it is for. A good
human DM doesn't control the dice either; that's the point.

### ⚠️ 2026-08-25 — half of this is currently NOT TRUE. Read before trusting §1.

The decision that **the runtime is the agent** ([`../README.md`](../README.md)
§ *The engine*) removed the code. Each requirement was mapped to a replacement,
and **one of those mappings was wrong.**

| | claimed replacement | honest status |
|---|---|---|
| **dice** | a shell call | ✅ **genuinely solved.** External, unanticipatable. |
| **arithmetic** | a shell call | ✅ available |
| **rules** | retrieval from `library/` | ✅ fine |
| **turn loop** | a procedure in `DM.md` | ✅ fine |
| **binding results** | contract + roll log | ✅ was never code |
| **state** | *"files it reads back"* | ❌ **this does not replace the inversion** |

> **Reading was never the problem. Writing was.**
>
> The inversion was not about the model having reliable *recall*. It was about
> the model having **no authority over the exact layer.** A file the model reads
> back and then writes to is not that — it is the model with a notepad.

**Specifically:**

- `resolve` in §4 still reads *"deterministic. code, not model."* **There is no
  code in it.** The model does the arithmetic and then chooses what to write.
- **`ledger.jsonl` audits dice, not state.** Nothing catches `HP 48 → 44` being
  written as `48 → 46`.
- **The audit has no consumer.** It only works if someone forensically checks
  whether their own game cheated them, after the fact. Nobody does that twice.

**This is not a peer concern to context cost.** One is an optimisation; this is
the project's founding claim.

**Two honest paths, and one has to be taken:**

1. **Accept that the model owns state** — and stop calling this an inversion.
2. **Put one deterministic thing back** — a state file the model may only mutate
   through a script, which refuses to write without a justification and a roll
   reference. Drift becomes visible at write time instead of forensic. Roughly
   an afternoon.

**Path 2 is preferred, and it is deliberately NOT scheduled yet.** The grind
probe runs *naked* first ([`test-criteria.md`](test-criteria.md) §2) to find out
whether the model actually drifts and in which direction — because building the
gate first means hardening against an assumed failure.

*(Red-team, 2026-08-25.)*

### External is not the same as binding

External RNG stops the model **generating** a favourable number. It does nothing
about the model **reinterpreting an honest one**:

> *"You rolled a 4 — but the guard is distracted, so you slip past."*

That's fudging the consequence, not the die, and no amount of roll-integrity
engineering catches it. **The contract has to make results binding**, not merely
externally generated. This is the single most likely way a technically-correct
Seren still feels like it's cheating.

**But binding ≠ literal.** Interpreting a roll is the DM's actual craft, and a
contract that forbids it produces a worse DM, not a fairer one. The line sits
one level finer:

| | | |
|---|---|---|
| ✅ **interpretation** | *"You fail the lock — **and** you hear boots on the stair. You have one round."* | failure stands; the scene moves |
| ❌ **reversal** | *"You fail the lock — but let's say you get it."* | outcome flipped |

**The test is a single question: did the success/failure state change?**

If no, the model has **full latitude** — tone, cost, what it reveals, whether it
fails forward, what it hands the player instead. That is the job.
If yes, it cheated, regardless of how good the reason sounded.

Same split as facts-vs-telling below, drawn one level down: **zero authority over
the outcome, total authority over what the outcome means.**

**Audit, cheaply:** log every roll with its DC and its outcome to the session
log. Costs nothing, and makes softening detectable after the fact.

**On rolling inside an artifact** *(considered, deferred)*: it adds nothing for
integrity — a local RNG is exactly as un-influenceable. What it buys is
**theatre**: watching a d20 land is part of playing D&D and *"you rolled 17"* is
not the same experience. That's a real reason to build it, but a feel reason,
not a fairness one — so it's a later problem.

### But do not over-apply this

Read alone, the rule above builds a rules engine that types prose. **The DM is
not just an arbiter — they're the storyteller**, and that is the half of the job
worth having.

The split is clean, and it must be stated in the contract or the constraints
will quietly eat the storyteller:

| | authority | who holds it |
|---|---|---|
| **facts** — numbers, dice, rules, what is true | **zero** for the model | code, RNG, the rules library, canon |
| **telling** — description, NPC voice, pacing, what the moment *feels* like | **total** for the model | the model, shaped by `DM-persona.md` |

The model never decides *whether the arrow hits*. It decides **everything about
what that looks like**, and it should be given real latitude there — that's not
a leftover after the constraints, it's the product.

`DM.md` constrains column one. **`DM-persona.md` empowers column two.** A
contract that only constrains produces a competent, lifeless DM; that failure is
just as fatal as the confabulating one, and much easier to walk into while
trying to fix the first.

---

## 2. Sheet vs State — the distinction everything rests on

These are **two different artifacts with two different lifecycles**, and
collapsing them is the single most likely way to build this wrong.

| | **sheet** | **state** |
|---|---|---|
| what | the template — what Ser'en *is* | the live instance — what Ser'en *currently has* |
| example | "Cosmic Omen: 4 uses per long rest" | "2 uses left" |
| example | "Max HP 101" | "48/101, no temp" |
| example | "knows Guardian of Nature" | "concentrating on Guardian of Nature, 4 rounds elapsed" |
| changes | on level-up, rarely | constantly, mid-combat |
| lives in | `characters/*.md`, version controlled | runtime, ephemeral |

State is derived from the sheet at session start and diverges immediately.

---

## 2b. Master → campaign build → state

Sheet-vs-state is actually **three** layers, not two. Play happens in a *new*
campaign, so the imported characters are masters, and each campaign derives a
**devolve** at whatever level that campaign is running.

| layer | what it is | lifecycle | lives in |
|---|---|---|---|
| **master** | the character at their canonical (highest) level | changes on level-up | `characters/*.md` |
| **campaign build** | the same character *devolved* to the campaign's level | fixed per campaign, changes on level-up | `LIVE/<campaign>/builds/` |
| **runtime state** | current HP, slots, conditions, concentration | changes every round | ephemeral, never persisted |

### What makes devolving mechanical rather than guesswork

Most of it is derivable, given the rules library:

- **class features** — known by level from the SRD
- **ASIs / feats** — **4, 8, 12, 16.** ⛔ **NOT 19** — that is `Epic Boon`. And **not “fixed”**: Fighter also gets 6 and 14, Rogue also 10. *(Corrected 2026-08-27 against SRD 5.2 — [`../library/2024/core.md`](../library/2024/core.md). It was a 2014 fact in a 2024 project.)*
- **spell slots, cantrips known, spells prepared** — all table lookups
- **subclass** — gained at **3** by all twelve classes. ⛔ **Its FEATURES are per-class and only four of twelve land at 6/10/14** — Cleric is 6/17, Fighter 7/10/15/18, Paladin 7/15/20, Rogue 9/13/17. *(Corrected 2026-08-27 — table in [`../library/2024/core.md`](../library/2024/core.md).)*

**The part that is NOT derivable is equipment.** Nothing in the rules says which
magic items a level 5 version of Korth should have, and handing a level 5
character a Rod of the Pact Keeper +2 wrecks the campaign. Item loadout is a
**per-campaign DM decision** and must be authored, not computed.

So: `devolve(master, level)` → mechanically correct chassis, **plus a required
manual equipment pass.** The engine should refuse to produce a build with items
inherited blindly from the master.

### Gear is a statement of shape, not a packing list

**Stated explicitly 2026-08-24, because it was implied everywhere and written
nowhere.**

A master sheet's inventory records **what kind of character this is** — the
power level they play at, the tricks they reach for, what they carry that says
something about them. It is **not a list of objects to import.**

At campaign start the DM **transposes**: same *kind* of item, specific to this
campaign and this location.

| master has | transposes to |
|---|---|
| Ring of Shooting Stars | *some* very-rare utility item that fits this world |
| Gnome-sized Black Dragon Scale Mail | armour from **this** campaign's monster, resized |
| Cli Lyre | this setting's named instrument |
| Stone of Good Luck | whatever this world's luck charm is |

**This dissolves a problem that looked serious.** The roster has a Ring of
Shooting Stars on **four** sheets and gnome-sized dragon mail on **three** —
which reads as a data error until you realise the master layer never promised
uniqueness. Four characters who each carry *a very rare utility item* is a
perfectly coherent statement. Four characters carrying *the same ring* is only a
problem if you import literally, and you never should.

**The same pattern, one level up, is how the world gets built:** enter a town →
generate its core NPCs; start a campaign → generate the party's loadout. In both
cases a **template** produces an **instance**, and the instance is what has
state. See [`npc-containers.md`](npc-containers.md).

> **`characters/` is a template library, not a save file.** Nothing in it is the
> live state of anything. That's why it can hold contradictions the campaign
> layer resolves.

### One thing the masters need for this to work

Level attribution — *what was taken at which level*. D&D Beyond doesn't record
it retroactively and neither did the import, so for now it's reconstructed from
the rules. Where a character has something the rules can't place (a homebrew
feature, a campaign boon), the master file must say **which level it arrived
at**, or devolve will either drop it or hand it over too early.

---

## 3. Fog of war — what's TRUE vs what's KNOWN

Easy to miss and it *will* bite. If all canon sits in one context blob, the model
will leak the dungeon's secret in its narration without ever noticing it did.

Every canon fact carries a visibility:

- `true` — the world model. DM-only.
- `known` — the player has learned it in play.
- `suspected` — the player has a theory, possibly wrong.
- `false` — the player believes something untrue. **Keep these.** A player
  operating on bad information is good drama, and the DM must not accidentally
  correct it.

The model receives the `known` and `suspected` sets as *what the character can
reason from*, and the `true` set as *what it must not contradict or reveal*.
Those are different instructions on the same data and must be labelled as such.

---

## 4. The turn loop

```
player input
   -> intent           what is being attempted, in game terms
   -> adjudicate       does this need a roll? which? DC? adv/disadv?
   -> ROLL             external RNG. model does not see it coming.
   -> resolve          apply to state. deterministic. code, not model.
   -> narrate          model describes the outcome it was HANDED
   -> record           append to session log; promote canon if warranted
```

**The one thing that must survive any implementation:**

- **The model narrates a result it did not choose.** This is the whole game.

### ⚠️ Corrected 2026-08-25 — the "separate calls per stage" note

This section previously called for **separate model calls per stage** —
adjudicate, update, narrate, plus a verification pass — as *"unaffordable at
commercial scale, completely fine here."*

**That contradicts the decision that the runtime is the agent.** One agent in one
loop does not give you four differently-constrained calls with an independent
verification pass. Getting that would mean orchestrating it, which is the
application [`../README.md`](../README.md) § *The engine* decided not to build.

**Both cannot be true.** For now the loop above is **one agent executing a
documented procedure**, and the verification pass does not exist. If separate
calls are ever wanted back, they arrive with an application, not before it.

⚠️ **And `resolve` still says *"deterministic. code, not model."* There is
currently no code in it.** See §1.

*(Red-team, 2026-08-25.)*

---

## 5. Session boundary — what persists

This is where SelfActual **vault principle #7** (*write at completion, not real
time*) meets a game whose HP changes every round.

**Ephemeral — never written to the pod:**
- current HP, temp HP, expended slots, conditions
- initiative order, positions, round counter
- concentration, active durations

**Persisted at session end:**
- session log — what happened, decisions, open loops, next steps
- canon promotions — facts established, NPCs met, promises made, reputation
- character state deltas that survive a long rest (level, inventory, boons)
- clock advancement (see fronts, below)

Respect that line and #7 is satisfied. Blur it and you've built something slow
that also breaks your own rules.

---

## 5b. The world state files

A factual, stateful world the DM plays *within*, rather than one it re-invents
each session. Three file types, each answering a different question:

```
world/
  locations/
    <place>/
      charactermap.md     WHO IS HERE — an index, not the people themselves
      state.md            what is true about this place right now
  npcs/
    <npc>/
      state.md            what is true about this person right now
      secrets.md          what the DM knows and the player does not
  characters/
    <pc>/
      secrets.md          DM-side subplot hooks about a PLAYER character
```

**`charactermap.md` is the load-bearing one.** It answers *"who is here"* without
loading every NPC in the world into context. The DM reads the map, then pulls
only the `state.md` files for people actually present. That is what keeps a
long campaign inside a context window.

**`secrets.md` on a PC** is the subplot engine — a curse they don't know about,
a lie in their backstory, who is actually hunting them. Essential in solo play,
where there are no other players to carry hidden threads.

### The honest caveat about secrets

**Running locally, `secrets.md` is honour-system.** The player owns the
filesystem and can open the file. It works the same way not peeking behind a DM
screen works: by agreement.

### ⚠️ Corrected 2026-08-25 — the pod does NOT fix this

This section previously claimed that sub-pod ACLs turn the honour system into a
real boundary, and called it *"the first feature that actually requires the
pod."*

**That is wrong.** The player is the operator, and the operator administers the
pod. **ACLs do not partition someone from their own vault.** For an audience of
one it is the same honour system with more steps and a network hop.

**It only becomes a real boundary with a second person** — a DM and a player who
are different people. That is a different product, and nothing in Seren
currently aims at it.

**So `secrets.md` is honour-system, full stop**, and will stay that way for as
long as Seren is single-player. It works the way not peeking behind a DM screen
works: by agreement. That is fine — it just is not an argument for the pod.

Local-first remains correct. The pod still matters for multi-device play and for
release; it does not matter for this.

*(Red-team, 2026-08-25.)*

---

## 6. Campaign as fronts and clocks, not a script

The two failure modes are **railroading** (model drags you back to the plot) and
**mush** (model says yes to everything, nothing has weight). Both come from
writing a *story*.

Write **agendas** instead — Blades in the Dark / Dungeon World structure:

```
front:  the Sundered Choir
  wants:    to wake the thing under the barrow
  doing:    buying up salvage rights along the coast
  clock:    [####------]  advances when the party is elsewhere
  if full:  the barrow opens; every coastal node changes state
```

The DM contract holds what is **true** and what is **in motion** — never what
happens next. Improvisation is then bounded by *causality* rather than by plot,
and going off-script isn't a deviation, it's input to a world that was already
moving.

---

## 7. Decided: theatre of the mind ✅

**No tactical grid.** Decided 2026-08-24 — Jay doesn't like them, and the
architecture is markedly simpler without one:

- **position is not persistent state** — no coordinates, no movement tracking
- **maps are illustration, not game data** — Claude Design output is sufficient,
  and no VTT is needed. A map can sit open in artifact view as **shared
  reference** while the DM describes where you are; it's a picture both parties
  can point at, not a surface anything is tracked on.
  - ⚠️ **The displayed map must be the PLAYER's map, not the DM's.** A reference
    image showing the full dungeon leaks it — same fog-of-war split as canon
    (§3), applied to an image. Two map layers: what's been explored or told, and
    what's true. Only the first is ever rendered.
- **encounter state shrinks to initiative order + rough zones**
  ("in melee", "at range", "behind the pillar")
- **`charactermap.md` is about who is *present*, not where they're standing**

This also removes the main reason to build a dice artifact: without a grid it
would be a die roller, not a VTT.

**Consequence to watch:** several abilities in the roster are explicitly
positional — Sculpt Spells (Jornis, "choose 1 + level creatures"), Manifest
Wrath of the Sea (Kree, 10-ft emanation), Spirit Guardians (Reg), Polearm Master
reach (Arthryn). Theatre of the mind has to adjudicate "who's in the blast"
narratively and **consistently**, or those features quietly stop meaning
anything. That's a contract problem, not a state problem.

## 8. Open architectural questions

1. **Do companions get full agency?** DM-run companions are simpler but drift
   toward the DM playing with itself.
2. **Where does adjudication authority sit** when the model proposes a ruling the
   code can't validate? Needs an explicit fallback — probably "ask the player,"
   which is what a real DM does anyway.
