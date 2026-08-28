<!-- Copyright (c) 2026 Jeremy Wright. All rights reserved. Published for review only; no licence granted. See LICENSE.txt -->

# campaign-start.md

**How a filed campaign becomes a living world.**

> ## The one rule
>
> **This runs once, before play, and never again.**
>
> Everything else in Seren is a **template layer** — 42 role templates, 26 feat
> shapes, 10 item shapes, 14 character masters, the container spec. **This
> document is the recipe that consumes them and emits a campaign.**
>
> `DM.md` references this file as a **non-loading pointer**: the folder was built
> before play, the DM needn't read this, and **must not re-run it.**

---

## 0. Before you start

Two prerequisites, both hard:

1. **A campaign is chosen** from [`../campaigns/candidates/`](../campaigns/candidates/), and **its own licence page has been read** — not the publisher's general terms, the specific file's. Anything not explicitly redistributable stays in [`../campaigns/reference/`](../campaigns/reference/) and never enters the repo.
2. **A level is chosen.** Everything downstream depends on it, and it is not easily changed afterwards.

---

## 1. Create the folder

```
LIVE/<campaign>/
  campaign.md            premise, tone, session-zero outcomes
  DM-persona.md          WHO is running it — see dm/persona-format.md
  fronts.md              what is in motion — agendas + clocks
  ideas.md               what COULD be wired in, untriggered
  builds/                the party, devolved to this campaign's level
  canon/
    locations/<place>/
      state.md           what is true here
      charactermap.md    who is here — links only
      npcs/              containers, created ON CONTACT (empty at t=0)
    antagonists/         interaction logs for the activated nemeses (§5b)
                         a SIBLING of locations/ — antagonists travel
    characters/<pc>/
      secrets.md         DM-side, campaign-specific
  state/                 THE LIVE GAME — written continuously
    party.md             t=0, from the builds
    scene.md             first scene
    queue.md             on the first uncaptured NPC
    facts.jsonl          t=0, EMPTY — SRN-11
    ledger.jsonl         t=0, EMPTY — appended every roll, forever
  sessions/              session logs
```

> ### ⛔ THE ROOT IS `LIVE/`, NOT `campaigns/` — corrected 2026-08-27
>
> **This tree was built on `campaigns/<name>/` from the day it was written.**
> [`../LIVE/README.md`](../LIVE/README.md) is the authority and says the
> opposite:
>
> ```
> campaigns/modules/<slug>/   the module      · template · portable · MAY SHIP
> LIVE/<campaign>/            the playthrough · instance · yours   · NEVER SHIPS
> ```
>
> ⚠️ **So this section was instructing the generator to write a player's live
> game into the directory that ships** — the same class of problem as §2's
> content-lines leak, and larger, because it is the whole tree rather than one
> file. `.gitignore` already excludes `LIVE/*`; it has never excluded a campaign
> folder under `campaigns/`.
>
> ### ⚠️ And `state/` was missing entirely
>
> **The build-test's PASS list requires *"`state/` and `sessions/` exist, with
> `facts.jsonl` and `ledger.jsonl` present and empty."*** ⛔ **This procedure
> never created `state/` at all**, so as written it could not pass its own test.
>
> ⭐ **Three files described this tree and no two agreed** — this section,
> `LIVE/_SAMPLE/`, and `test-criteria.md` §1. **SRN-42.** Reconciled here; this
> tree is now canonical and the other two follow it.

### ⚠️ A correction to the container spec

[`npc-containers.md`](npc-containers.md) §1 puts containers at
`canon/locations/…` at the **top level**. That's wrong, and this is the fix:

**Canon is campaign-bound.** What's true in one campaign isn't true in another.
So `canon/` lives **inside the campaign folder**.

The top-level [`../canon/`](../canon/) holds something different — **portable
canon** that travels with a character across campaigns:

| top-level `canon/` | `LIVE/<campaign>/canon/` |
|---|---|
| who a character **is** — Ser'en's `bible.md`, her `secrets.md` | what this campaign **established** — NPCs met, promises made, places seen |
| imported setting reference | discovered state |
| **template layer** | **instance layer** |

Same split as sheet-vs-state, one level up. *(Fix the path in
`npc-containers.md` §1 when convenient — the design is right, the location was
wrong.)*

---

## 2. Session zero → `DM-persona.md`

**Do this before writing anything mechanical.** It sets tone, and tone changes
what you author afterwards.

Session zero produces **the persona, not the contract**. `DM.md` is shared
across every campaign and does not change here.

**Write it to [`../dm/persona-format.md`](../dm/persona-format.md) v2** — five
parts, in this order: **identity · seven dials · moves · a falsifiable prediction
· when this persona is wrong.** That file carries the fill notation, the
three-dial floor, and the six-step derivation; **do not restate them here.**

**Worked example:**
[The Registrar](../campaigns/modules/a-wild-sheep-chase/DM-persona.md).

**Without this the AI defaults to generically pleasant**, which is the one thing
no good DM is. Architecture §1: the contract constrains, the persona empowers.

> ### ⛔ What session zero must NOT write into this file
>
> **Content lines. Lethality. Telegraph density. How hard the DM pushes back.**
>
> ⚠️ **These are the PLAYER'S and they live in
> [`../dm/table-agreement.md`](../dm/table-agreement.md)**, which every campaign
> inherits. **The conversation happens once, not at the top of every campaign.**
>
> ⭐ **It is a privacy rule, not a tidiness one.** A campaign folder can be
> zipped and handed to someone else — **write a person's content boundaries into
> it and you ship them to strangers.**
>
> *(This paragraph replaces a bullet list that instructed exactly that leak.
> Corrected 2026-08-26 when the persona format went to v2.)*

> ### ⚠️ The seed cannot fill this yet
>
> `dm_persona_seed` carries **six v1 fields**, and **four of the seven dials have
> nothing upstream to derive from** — roll frequency, failure texture, canon
> generation, callback appetite. **The Registrar came back with all four marked
> `unset — no source`.**
>
> ⛔ **Until the seed schema catches up, session zero must ASK for those four
> rather than infer them**, and record `no source` if the player has no view.
> **SRN-37.**

---

## 3. Author the fronts

**Agendas, never plot.** Architecture §6 — write what factions *want* and what
they're *doing*, with a clock that advances when the party is elsewhere.

```
front:  the Sundered Choir
  wants:    to wake the thing under the barrow
  doing:    buying up salvage rights along the coast
  clock:    [####------]  advances when the party is elsewhere
  if full:  the barrow opens; every coastal node changes state
```

**Two to four fronts is plenty at start.** Seed `ideas.md` from
[`../campaigns/IDEAS.md`](../campaigns/IDEAS.md) — the pool harvested from the
characters' own sheets — but **only copy what fits this campaign.** An idea
records its **trigger** and its **cost**; a spent idea is *promoted* to a front
or to canon, never left in the pool.

**Antagonists attach to fronts, they are not fronts.** If a villain's death
would end the plot, they're a front. If they'd just be gone, they're an
antagonist. See [`npc-containers.md`](npc-containers.md) §8.

---

## 4. Devolve the party

**`devolve(master, level)` → `builds/<character>.md`.** Architecture §2b.

**Derivable, do it mechanically:**
class features by level · ASIs · spell slots, cantrips and prepared counts ·
subclass features · HP — **all of it is in
[`../library/2024/core.md`](../library/2024/core.md)**, and ⚠️ **the ASI and
subclass levels this file used to state inline were wrong.** Do not restate
them; look them up

**NOT derivable — this is the manual pass:**

> **Equipment.** Nothing in the rules says which magic items a level 5 Korth
> should carry, and handing a level 5 character a Rod of the Pact Keeper +2
> wrecks the campaign.

**Gear transposes, it does not import.** The master's inventory records *what
kind of character this is*, not a list of objects. Ring of Shooting Stars
becomes *some* very-rare utility item that fits **this** world. Use the ten
shapes in [`../library/homebrew-items/`](../library/homebrew-items/) — and
`provenance` is the transposition key: knowing an item has 3 charges tells you
nothing, knowing it's *a noble house's recall token* lets you build this
campaign's version immediately.

**The engine should refuse to emit a build with items inherited blindly.**

### The devolve is a CONVERSATION, not a computation

**Added 2026-08-25 (Jay).** The section above reads as though the AI derives a
build and hands it over. **It is the player's character**, and everything the
master under-determines is theirs to decide.

> **Anything the master under-determines is a conversation, not an inference.**

**But a conversation with a recommendation in it.** *(Jay, 2026-08-25.)* The
campaign-start AI is **not the DM** — different job, different session, and it
may reason freely about the character in a way the DM at the table should not.
It should arrive with a proposal:

> *"At level 4 I'd prepare these six and drop Counterspell — nothing here needs
> it and you lose the reaction. Sound right?"*

**Recommend, then confirm. Never interrogate, and never auto-fill.** A blank
questionnaire at session zero is exhausting and produces worse answers than a
good proposal the player pushes back on. The player's job is to disagree, not to
originate.

**Three consultations at campaign start, not one:**

| | why it can't be derived |
|---|---|
| **equipment** *(above)* | nothing in the rules says what a level 5 version carries |
| **spell selection** | ⚠️ **not subtractive, even going down.** A level-11 wizard's prepared list was chosen for level-11 problems; at level 4 with three slots you cannot take the first three off it. The selection logic changed, not just the count. Same for invocations, domain picks, manoeuvres, anything chosen in context. |
| **signature feat** *(§5)* | it defines who they are |

**Going UP is strictly harder than going down.** Beyond the master's level
nothing has been chosen at all — every ASI, feat, subclass feature and spell is
a fresh decision. **Never auto-fill those.** Ask.

### Starting from level 1

**Most of the mechanical work collapses.** A level 1 character has a handful of
features, no subclass, and two spells.

⚠️ **But trivial is not the same as good.** A devolve that does almost nothing
also *tests* almost nothing — and levels 3–5 are where the interesting machinery
lives (subclass at 3, first ASI at 4). If the point of a run is proving the
devolve works, level 1 proves the easiest possible case.

**Say out loud that the master is not binding.** Climbing back from 1, the
choices will differ from the level-11 sheet. **That's correct.** These are
structures, not scripture.

---

## 5. Signature homebrew feats

**One per PC**, from [`../library/homebrew-feats/`](../library/homebrew-feats/).

Pick a **shape** — aura, trade, bond, token, pool, passenger — start from the
`## The hook` line rather than the mechanics, instantiate it for *this* world,
and **decide when it unlocks.**

**Write it into the campaign, not onto the character sheet.** The character is a
template; the feat is an instance.

**The constraint, held hard:** a signature feat says *who you are*, it does not
raise your numbers. Moonwell Presence is the model — it makes Ser'en legible,
not stronger. Turn these into +2 damage riders and every PC gets a power bump.

---

## 5b. Activate the antagonists

**Added 2026-08-24.** This step was missing — the six nemeses in
[`../npcs/antagonists/`](../npcs/antagonists/) are a template layer, and nothing
said who consumes them. This does.

**Pick two or three. Not six.**

Six is the *bench*, not the roster. Every antagonist activated at t=0 is one the
player has to hold in their head from session one, and the whole value of the
tier is *"oh, it's him again"* — which needs a small enough field to recognise.
**Activate more later; the bench does not expire.**

### Pick on availability first, then on axis

1. **Check `attaches_to:`.** Four of the six hang off a specific PC. If that PC
   is not in the party, either use the antagonist's `fallback:` or leave them on
   the bench. Two are `attaches_to: [party]` and always work.
2. **Do not activate two on the same axis.** The six are spread across what they
   *want* — extraction, obstruction, vendetta, seduction, collateral, correct —
   precisely so that a small selection generates different scenes. Two vendettas
   is one nemesis with two faces.
3. **Prefer one that cannot be fought.** Ilma and Teodor generate scenes no
   combat encounter does, and a bench of three brawlers wastes the tier.

### Then, for each one activated

- [ ] **Fill `grudge:`** — one line, **party-relative**, written against the
      actual party. The `grudge_seed:` in the file is the character-level fact it
      hangs on and is **not** a substitute for it.
- [ ] **Transpose anything they carry.** Corwen's inherited weapon comes off a
      PC's master sheet; the item is a *kind*, not an object. Architecture §2b.
- [ ] **Answer the forks in their `-secrets.md`**, where one exists. Maelis,
      Ossa and Iselde each have a decision the campaign must make **before** they
      are used — improvising it in the scene where it lands is how the reveal
      gets wasted.
- [ ] **Create the interactions log**, empty:
      `canon/antagonists/<slug>-interactions.md`

### Antagonists are not fronts, and this is where that gets enforced

**If activating one requires inventing a faction, a war, or a place, stop.** The
templates leave world details deliberately unnamed so the campaign can fill
them — but filling them with an *organisation with an agenda* means you have
written a front (§3) and given it a face. The test from §3 holds: **if their
death would end the plot, they are a front.**

---

## 6. The starting location

**This is almost nothing, and that's the design working.**

```
canon/locations/<place>/
  state.md           what is true here — a few paragraphs
  charactermap.md    EMPTY, or one or two named residents
  npcs/              EMPTY
```

**Do not populate the town.** People are created **on contact**, from a role
template plus the trait tables, and written at session close. A town with forty
pre-written residents is forty strangers nobody will meet.

Name two or three people the premise actually requires — the innkeeper the
adventure opens on, the patron who hires the party — and stop.

---

## 7. What is NOT created now

Everything below appears **during play**, written at session close:

| appears | when |
|---|---|
| NPC containers | first real contact |
| `<npc>-interactions.md` | first exchange worth recording |
| canon facts | established in play, with visibility tags |
| session logs | session close |
| PC `secrets.md` | when a subplot needs somewhere to live |
| new locations | when the party goes somewhere |
| promotions to `named` | when the player remembers a name unasked |

---

## 8. The t=0 manifest

**Checklist. If any of these is missing, play should not start.**

- [ ] `campaign.md` — premise, tone, session-zero outcomes
- [ ] `DM-persona.md` — voice, lethality, pacing, content lines
- [ ] `fronts.md` — 2–4 fronts with clocks
- [ ] `ideas.md` — seeded, each with trigger and cost
- [ ] `builds/` — one per PC, at the campaign's level, **equipment pass done**
- [ ] one starting location with `state.md`
- [ ] `canon/locations/` and `sessions/` exist and are empty
- [ ] the campaign's licence checked and recorded
- [ ] signature feat chosen per PC, with its unlock condition
- [ ] **2–3 antagonists activated** — `grudge:` filled, secrets forks answered,
      empty interactions log created in `canon/antagonists/` *(§5b)*

---

## 9. Hand off to the DM

Once the manifest is complete, this document's job is finished.

`DM.md` carries the write-boundary clause, which is the only trace of this
procedure that survives into play:

> **The campaign folder was constructed before you by `campaign-start.md`. You
> do not need to read it, and you must not re-run it.**
>
> **You may write:** NPC containers, interaction logs, session logs, canon
> promotions.
>
> **You may never create:** fronts, builds, locations that were not authored,
> or campaign structure.

**The reference is deliberately non-loading.** It exists so the DM knows the
structure is intentional rather than incidental — a bare prohibition gets
rationalised around in a long session, a reasoned one doesn't. It is not an
instruction to go and read this file.

**The procedure builds the world. The contract governs what happens inside it.**
