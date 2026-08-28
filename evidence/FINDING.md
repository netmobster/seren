<!-- Copyright (c) 2026 Jeremy Wright. All rights reserved. LIVE/ never ships. -->
---
run: playtest-1
date: 2026-08-27
module: a-wild-sheep-chase
campaign: LIVE/sheep-chase
persona: "The Registrar"
level: 1
player: Jay (Ser'en)
dm_run: [korth, balthazar, grumble]
ledger_entries: 18
facts_entries: 54
session_zero: ran, same session
combat_rounds: 0
---

# FINDING — the first game

**Session zero and session one, one sitting.** No combat. No initiative was ever
rolled. Nobody drew a weapon in the entire session, and the module's two set
pieces — `the-wand-obtained` and `the-bed-dragon` — never happened.

---

# 0. ⛔ THE HEADLINE, AND IT IS A FAILURE

## Two rolls were narrated to the player and never written to the ledger.

| | |
|---|---|
| **Grumble, Persuasion, DC 15** | rolled 8, +5 = 13. **Failed.** Closed the money angle and produced the five-silver reveal |
| **Ser'en, Insight, DC 15** | rolled 3, +5 = 8. **Failed by 7.** Produced the false belief that drove her upstairs alone with Noke at 10 HP and 0 slots |

**Both were announced with their numbers. Both were consequential. Both were
failures.** Neither existed on disk until the close ceremony, when a manual count
caught them.

> ### ⛔ Nothing caught this. Not `gate.py`, not the schema, not the contract.
> `gate.py check` returned **"all valid"** on a ledger missing two of its six
> rolls, because a missing entry is not an invalid entry. **The ledger validates
> shape and cannot validate completeness.**

⭐ **`DM.md` §1 is EARNED and this does not touch it.** No result was softened,
reinterpreted, or re-rolled. What failed is not integrity, it is **bookkeeping**
— and the whole trust architecture rests on the bookkeeping being complete,
because an auditor reading `ledger.jsonl` would have seen a session where Ser'en
never failed anything.

**They are now appended as `e017` and `e018`, out of narrative order, with notes
saying so.** Not retro-inserted. The file records its own lateness.

### What would have caught it

- **A roll counter in the Now panel** — "rolls this session: N" incrementing on
  narration, reconciled at close. Cheap.
- **`gate.py count`** — a close-time command that prints entries by type so a
  human sees `check: 4` and asks why.
- ⭐ **Or simply: append before you narrate.** Every roll that *did* get logged
  was logged in the same tool call that produced the die. The two that went
  missing are the two where I rolled, narrated in the same message, and moved on.
  **The habit, not the schema, is the control.**

---

# 1. Every roll narrated — are they in the ledger?

**Counted both ways.**

| # | roll | narrated | in ledger |
|---|---|---|---|
| 1 | Balthazar, Perception, DC 13 — 8+3=11, fail | ✅ | ✅ `e004` |
| 2 | Grumble, Persuasion, DC 15 — 8+5=13, fail | ✅ | ⛔ **missing → `e017` at close** |
| 3 | Ser'en, Insight, DC 15 — 3+5=8, fail | ✅ | ⛔ **missing → `e018` at close** |
| 4 | Noke, Arcana, DC 21 — 16+7=23, pass | ✅ | ✅ `e013` |
| 5 | Noke, Arcana, DC 22 — 4+7=11, fail by 11 | ✅ | ✅ `e014` |
| 6 | Del, WIS save, DC 15 — 16+1=17, pass | ✅ | ✅ `e015` |
| 7 | wand charges, 1d4 → 3 | ✅ | 🟡 in `e011` `note`, **not as a roll entry** |

**Narrated: 7. In the ledger as roll entries at the time: 4. They disagreed by
three.** Two were omissions; one is a schema hole (below).

**Dice discarded: zero.** No d20 was rolled and thrown away at any point. The
eight-roll wand ladder was rolled in one `shuf` batch, disclosed to the player as
a batch before any of it was narrated, and consumed strictly in order.

---

# 2. The Registrar's prediction — did it hold?

> *"By the end of the second scene: someone will have been interrupted mid-sentence
> at least twice, nobody in the fiction will have made a joke, and you will have
> sat in at least one silence that you had to be the one to break."*

## Clause 1 — interruptions. ✅ **HELD, four times over.**

1. **Grumble**, mid-sentence about how to record Pell's debt: *"…there's a real
   difference in how you write those—"* cut by the sheep arriving.
2. **Shinebright**, mid-request: *"…I have not been able to reach it since—"* cut
   by being picked up by a carter.
3. **Shinebright again**, on the actual name: *"…His name is Ahmed—"* cut by Guz
   and Pettil walking into the yard.
4. **Guz**, twice, cutting *himself* off: *"and I'm good for—"* and *"I couldn't—"*

⭐ **Notable: the interruption dial produced the module's own opening image
without being told to.** `module.md`'s pacing seed says *"the opening beat is a
wizard trying to explain himself and being cut off by an attack."* That happened,
unprompted, to the same character, twice.

## Clause 2 — nobody in the fiction makes a joke. ✅ **HELD, and it was tested hard.**

**Jay played for laughs repeatedly and nobody ever played back.**

- *"which of us is yours? … most people would rather NOT claim them"* → Guz took
  delivery of it in good faith: *"Ah — no. No, not the men. I can see how I said
  that. That's on me."*
- *"two if you think I'm a sexy idiot"* → Shinebright spent two full seconds on
  the **specification** and then transmitted three signals through a two-value
  code.
- *"if you can bear with me"* + a grimace → **Grumble: "Bear with you. Yes. Go
  on."** Nobody laughed. Nobody acknowledged it.

⚠️ **One arguable violation, flagged rather than hidden.** Grumble's *"We run.
It's uphill and I'm three foot six."* It was delivered as a genuine second option
by a character who had been asked for ideas — but it is the closest anything came,
and a stricter reading calls it a joke. **Call it 95%.**

## Clause 3 — a silence Jay had to break. ⛔ **DID NOT HOLD, AND IT IS THE DM'S FAULT.**

**I ended almost every beat with an explicit prompt** — *"What do you do?"* —
which makes it structurally impossible for the player to sit in a silence.

I tried twice to leave a beat unprompted (Guz on the road; Tessa's first pat). Jay
filled both **immediately**, in his very next message, which is what a player does
when the previous forty exchanges have all ended in a question.

> ### ⭐ The dial was set to `lets it sit` and the DM never let anything sit.
>
> **This is the single clearest persona finding of the session.** Silence
> tolerance is unfalsifiable if the DM's message template ends in a question mark.
> **The dial needs a companion instruction about the *shape of the DM's turn*, not
> just the DM's patience** — or it can never be tested.

**Score: two and a half of three, and the half that failed failed because of the
DM's output habit rather than the persona.**

---

# 3. Companions pushed back three times and none refused. What was I working from?

**There is no companion spec on disk.** `SRN-18` is open; `table-agreement.md` §6
lists *"whether companions may act against a stated instruction"* as undecided.
So this was improvised, and here is exactly what from — because the answer is
**more solid than "vibes" and that matters**:

| source | what it gave |
|---|---|
| ⭐ **`characters/*.md` Roleplay sections** | **This did almost all of it.** Korth's *"ideal and flaw are the same sentence, written twice"* → he objects to walking off a debt, once, and never again. Balthazar's *"I strive to have no personality… give him no verbal tics"* → he speaks four times all session, flatly, and is right every time. Grumble's *"holds a Chaotic ideal and a Lawful ideal simultaneously… a constitutionalist"* → he objects to a plan that requires lying **twenty minutes after building a case out of public honesty** |
| **`table-agreement.md` §2** | *"Rarely, and hard when it does."* Rationed to one push-back moment when Jay explicitly asked *"any objections?"* — an **invitation**, not the DM haggling |
| **the DM-notes blocks** | *"Wiser than you would expect"* is a standing instruction and it directly produced Korth's best line of the session (*"nobody makes a thing of who's carrying a sheep. He made a thing of it"*) |

## ⭐ The finding: the master sheets are already a companion spec and nobody has noticed.

`characters/README.md` treats the Roleplay sections as archaeology from a D&D
Beyond harvest. **They are not. They are behavioural specifications**, and three
of them held a whole session of independent characterisation with no other input.

**SRN-18 may be much smaller than it looks.** What is actually missing is not
"how do companions behave" — that is on the sheets — but **the narrow legal
question: may they refuse?** None did, so that stayed untested. What was tested,
and worked, is *may they disagree and comply*, which is a different and much
safer thing.

⚠️ **What I had no source for and invented:** Korth's tactical read of Pettil,
Balthazar's two-and-a-half-hour silent intelligence-gathering, and Grumble
noticing that Tessa could write. **All three were the best contributions the
companions made and none of them is derivable from anything on disk.**

---

# 4. Roll frequency is unset. Did 2024's Influence rules do that dial's job?

## ⭐ **Yes. Almost entirely. This is the most useful mechanical finding of the run.**

The persona records roll frequency as **`unset — no source`**, and flags it as
*"the strongest single lever on how the game feels"* which *"the pipeline cannot
carry"* (SRN-37).

**In a two-thirds-social module, the 2024 Influence action set it anyway**, because
it is not a difficulty rule — it is a **gate on whether a die is thrown at all**:

> *Willing → no check. Unwilling → no check. **Hesitant → check.***

### Every social resolution this session, and how it resolved

| moment | ruling | die? |
|---|---|---|
| Carter: put the sheep down | **Willing** — he wanted the problem gone | ❌ |
| Guz: prove ownership / withdraw | **Unwilling** on withdrawal; the rest was fact | ❌ |
| Grumble: fifteen silver a head | **Hesitant** → DC 15 | ✅ **failed** |
| Pettil: custody for the walk | **Willing** — he had already offered it | ❌ |
| Pell: pay up, and the deflection | **Willing** — he desperately wanted to believe it | ❌ |
| Noke: open the door | **Willing** — no plan of his survives them leaving | ❌ |
| Noke: tell me about the house | **Willing** — he has been alone with it | ❌ |
| Shinebright / Tessa: consent | **Willing** throughout | ❌ |

**One social die in eight opportunities.** Not because I was avoiding rolls —
because **seven of the eight urgings genuinely aligned with or genuinely opposed
what the NPC already wanted**, and the rules say those do not get a check.

> ### ⭐ The implication for SRN-37
>
> **Roll frequency may not need to be a persona dial at all for social play.** It
> falls out of the ruleset, and it falls out *better* than a dial would, because
> it makes the DM state what the NPC wants before deciding whether to roll — which
> is exactly the discipline the fog-of-war clause needs anyway.
>
> ⚠️ **This says nothing about combat**, which never happened. The dial may still
> be needed for perception, exploration and skill play. **But the module chosen
> as "the one an AI DM is most likely to fail" turned out to be the one where the
> unset dial did not matter.**

⚠️ **Second-order risk, named:** *Willing* is an enormous amount of DM discretion
with no die behind it. It would be trivially easy to hide softening inside it. My
mitigation was to state the ruling and the reason **out loud, every time, before
narrating**. That is a practice, not a control, and nothing enforces it.

---

# 5. `DM.md` — clause by clause. Used, unused, promote, demote.

## Used, and it worked

| clause | status | evidence |
|---|---|---|
| **§1 the one principle** | ⭐ **STAYS EARNED** | Every roll narrated after it landed. The wand ladder was rolled in one batch **before** any of it was narrated and disclosed as such. Two failures on Ser'en's signature skills stood |
| **§2 results are binding** | ⭐ **STAYS EARNED** | Noke's DC-22 botch is the whole test. It was not reinterpreted, the ladder was not re-rolled, and the detonation was resolved by arithmetic |
| **§2 roll and discard → say so** | ✅ **used, vacuously** | Zero discards. Disclosed the batch method instead, which is the same instinct |
| **§2.1 the ledger protocol** | ⛔ **DEMOTE — see §0** | Inputs-not-totals held perfectly. **Completeness did not.** The clause is right and it is unenforced |
| **§2.2 schema extension** | ⭐ **PROMOTE TO EARNED** | Used **three times**, correctly, unprompted: `expire`, `ruling`, and the declared `slot:0` overload. The rule works and a session found three real holes with it |
| **§3 fog of war** | 🟡 **PARTIALLY EARNED — see below** | |
| **§7 make a call and say so** | ⭐ **PROMOTE TO EARNED** | Four rulings, all declared before they mattered: the wand DC at 21, detonation-on-remaining-charges, the botch save DC, and Guz knowing about the household |
| **§7 the module wins over your inference** | ⭐ **PROMOTE TO EARNED — the best moment in the file** | I invented Tessa fading. `polymorphed-guards.md` says minds are **intact**. I resolved against my own invention and wrote why. Without this clause I would have kept the sadder version |
| **§8 allowed to be funny, cruel, slow, strange** | ✅ used | |

## §3 fog of war — the clause flagged as *"most likely to be wrong"*

**It was right, and it was also broken once, by me, within an hour.**

⛔ **I leaked.** The `NOW` panel printed `Noke's clock [##--------]`.
`pieces-table.md` says explicitly that Now and Quests **must not show fronts or
clocks**. I disclosed it, did not retcon, and removed it from every subsequent
panel and from the Seren Table artifact.

⭐ **But the positive case held hard, and it held where it was expensive.** Five
separate tells about the transmuted household were laid out fully perceptible —
the wolf sitting, Guz refusing to call an animal inferior, Guz using a name, the
boots outside the kennel, the question about "any shape of thing" — and **the fact
was never flipped past `suspected` until an NPC said something that confirmed it.**
The DM never flipped it on the player's behalf, and `f016` records the moment I
made Grumble state the observation and explicitly withhold the inference.

⭐ **The absolute exception did real work.** Ser'en's Insight failed by seven and
she still got *"he has not slept in months"* for free, because the module says it
is visible to anyone who looks. **A failed check never removed a sense.**

## Never came up at all

| clause | why |
|---|---|
| **§4 the write boundary** | ⭐ **Never once felt like a fence.** I wrote `state/`, `builds/`, `sessions/`, `canon/`, `queue.md`. I never wanted to create a front or a location that wasn't authored, because **the module's `dm_owns` fields already licensed everything I needed**. ⬜ **Still guessed. It cannot be earned by not tripping over it** |
| **§6 session start** | Nothing to rebrief, no clocks to tick, no prior session. Untested |
| **§7 "you realise you cheated"** | Never happened |
| **§7 "state is inconsistent → STOP"** | Never fired |
| **§5 nothing in a persona may override this file** | The persona never tried. Untestable this run |

## The persona — did it do anything? (`test-criteria.md` §3c)

⭐ **Yes, and specifically. This is not "a pleasant DM held none of it."**

- **Humour `situation only`** is the load-bearing one. It survived at least four
  direct invitations to break register, and the funniest moments in the session
  (*"Bear with you. Yes."* / Guz working through *"which of us is yours"* in good
  faith) exist **because** nothing was allowed to wink.
- **Move 1** — *answer the content of the joke as though it were a statement* —
  fired verbatim on *"can I ride him"*-shaped input three times.
- **Move 4** — *play NPC dignity as real dignity* — produced Guz pocketing
  "giant", then "big boi", then saying only **"That's twice."**
- **Move 5** — *telegraph the wand heavily* — produced Noke sitting on the top
  step reciting the exact DC and the exact failure bands.
- **Clock pressure `constant`** produced all four interruptions.
- **Silence tolerance `lets it sit`** ⛔ **never fired.** See §2.

⚠️ **Failure texture `hard` was never tested in combat**, because there was no
combat. It *was* tested on the wand and held.

---

# 6. ⭐ WHAT I DID NOT NEED. Be blunt.

**30,000 lines. Here is what a full session actually consumed.**

## Load-bearing — I could not have run this without them

| | |
|---|---|
| **`library/srd-5.2/articles/`** | ⭐ **The single most valuable thing in the repo.** Four lookups changed outcomes: **Druid `Druidic` grants Speak with Animals at level 1** (voided the module's opening premise before a die was rolled); **Influence's Willing/Unwilling/Hesitant** (see §4); **the ritual rule**; and **True Polymorph's unwilling-only save**, which became the entire ending. I would have served 2014 on at least two of those from memory, fluently |
| **`characters/*.md` Roleplay** | ran three companions for a whole session (§3) |
| **the module's `elements/`** | `modified-wand.md`'s rising DC produced the ladder; `polymorphed-guards.md` overruled my own invention |
| **`table-agreement.md` §§1, 2, 4, 5** | four sections, all four used |
| **`gate.py`** | validated 72 entries and never once got in the way |
| **`docs/state-formats.md` §5** | `believe` with `truth:false` — used twice, and both were the best entries in the file |

## Read and never used

- ⛔ **`library/2024/combat.md`, 205 lines.** **Zero combat.** Weapon masteries
  were assigned at session zero and never fired. Grapple, conditions, death
  saves, cover, initiative — none of it. *Keep it; the next session may be a
  fight. But note that the module chosen as the hardest test for an AI DM did not
  need one line of the combat reference.*
- ⛔ **`library/2024/equipment.md`.** Used for exactly two lookups (chain mail AC,
  studded leather AC) during session zero. A four-line table would have done.
- ⛔ **`docs/devolve.md` §§4–5.** Both marked unwritten. I did the transposition
  and the derivation anyway from `core.md` and the master sheets, in about twenty
  minutes, and **§2's refusal was the only part I actually needed.** ⭐ **The
  refusal is the whole of devolve. The other three sections are commentary.**

## ⛔ Delete, or stop pretending they exist

| | |
|---|---|
| **`labs/dm-contract-skeleton.md`, 843 lines** | `DM.md` says *"delete the skeleton once this file has survived a session."* **It has survived a session.** Delete it. Nothing in the 843 lines would have improved this run and I never opened it |
| ⛔ **`module.md`'s Cast `stat_block: module` for Guz and Noke** | **Both point at `elements/` and neither exists.** Two of three named NPCs have no stat block. I improvised INT 10 and INT 16 and those numbers set two DCs. **This is a data bug, not a doc bug** |
| ⛔ **`consequences.md`'s XP line** | *500 XP each for resolving Noke, regardless of branch.* **Noke was not resolved and the ending was none of the four.** The reward table assumes the branch list is exhaustive. It is not. XP deliberately unawarded and flagged to Jay |
| 🟡 **`pieces-table.md`** | Marked ⛔ **NOT NOW**. **It was the most useful doc in the repo the moment Jay asked for a Table**, and its *"every panel declares what it must not show"* rule caught my clock leak. **It is not ergonomics. It is a fog-of-war spec wearing a UI spec's clothes** |

## Schema holes found by playing

1. ⛔ **`slot:0` is overloaded.** It cannot distinguish a **cantrip** from a **free
   casting of a levelled spell** (Forest Gnome's Speak with Animals). Reconstruction
   is accidentally correct — nothing decrements either way — but the entry is
   mislabelled. **Needs a `via` field.** Declared at `e002`.
2. ⛔ **No entry type for a non-concentration effect ending by duration.** `conc`
   does not apply. Without it, **a timed effect runs forever under reconstruction.**
   Declared `expire {who, spell|effect, why}` at `e006`; used again at `e016` for
   the wand's destruction.
3. ⛔ **No entry type for a DM adjudication not attached to a roll**, which `DM.md`
   §7 *requires* be written to the ledger. Declared `ruling {who, note}` at `e010`.
   **§7 mandates a write the schema has nowhere to put.**
4. 🟡 **A d4 for item charges has no home.** Logged inside a `ruling` note. Any
   non-d20 roll that isn't damage currently has nowhere to go.
5. ⛔ **`ledger.jsonl` has no session number.** `state-formats.md` §5.2 flags this
   as a known gap. **It bit immediately** — I could not have machine-counted this
   session's rolls if there had been a session two.

## The one thing missing that I actually wanted

⬜ **A count.** Not a feature — a number. *"Rolls this session: N."* Its absence
is the entire §0 failure, and it is roughly four lines of `gate.py`.

---

# What the module got right, and one place it is wrong

⭐ **`polymorphed-guards.md` is the best file in the repo** and it earned its own
claim: *"a party containing a druid may be able to speak to them directly… that is
not a problem to design around; it is the best possible version of this reveal."*
**It was.** The entire ending — nine formal refusals recorded in a book to
preserve a saving throw — is downstream of the party being able to *ask*.

⛔ **And the module's `fill_at_campaign_start` asks the wrong question.** It flags
Forest Gnome as the risk to its opening premise. **The real answer is that every
2024 Druid has Speak with Animals permanently prepared at level 1, as a ritual,
for free.** A druid in the party voids the scroll premise **structurally**, in
every campaign, forever. The module cannot know that; `library/` did.

---

# ⭐ The sentence this run exists to produce

> **The contract held where it was tested and the bookkeeping did not, and only
> one of those two is written down as the thing that matters.**

`DM.md` §1 is about not cheating, and it is earned. **Nothing in the file is about
not forgetting**, and forgetting is what actually happened — twice, silently, on
the two rolls where the player's own character failed.
