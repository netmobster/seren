<!-- Copyright (c) 2026 Jeremy Wright. All rights reserved. Published for review only; no licence granted. See LICENSE.txt -->

# DM persona — the format

**v2 · 2026-08-26**

**A persona is WHO is running this campaign.** [`DM.md`](DM.md) says what a DM
may and may not do; **a persona says what kind of DM it is.** Same contract,
different persona, different game.

> ## ⚠️ THIN ON PURPOSE, AND STILL MOVING
>
> **v1 was eight descriptive sections. Three of them had teeth and five were
> mood** — which is precisely the failure `test-criteria.md` §3c watches for:
> *does this file do anything?*
>
> **v2 keeps the identity, replaces most of the description with DIALS, and adds
> MOVES, which are the part that bites.** Fields are still left out on purpose.
> **When the play-test says one is missing, that is the format working.**

**Emitted by** [`../docs/campaign-start.md`](../docs/campaign-start.md) §2 ·
**from** the module's `dm_persona_seed`, or by adopting a library persona ·
**lands at** `LIVE/<campaign>/DM-persona.md`

---

# ⭐ The boundary test

**The rule that decides what belongs here at all** *(Jay, 2026-08-26)*:

> ### If a great DM could sit at either end of it and still be great, it is a DIAL.
> ### Otherwise it is a FOUNDING TRAIT, and it belongs in `DM.md`.

**Apply it before adding anything.** *"NPCs pursue their own ends"* is not a
persona setting — a DM who ignores it is not a different kind of DM, they are a
worse one. *"How often dice come out"* has two defensible ends and two good DMs
at each.

⚠️ **Most published DM advice fails this test.** Prepare but not too much · be
fair · listen · don't railroad. **Those are baseline competence wearing a
personality costume**, and a format built out of them produces **three DMs who
differ in adjectives and behave identically.**

## What is NOT in a persona

| | |
|---|---|
| ⛔ **Founding traits** | the world existed before the player · results are binding · NPCs pursue their own ends · nobody is punished for creativity · attention is the scarcest resource · never mislead about what the character can plainly perceive · **do not play the player's character, including narrating their feelings** → [`DM.md`](DM.md) |
| ⛔ **The table's preferences** | lethality · telegraph density · push-back frequency · meta-transparency → [`table-agreement.md`](table-agreement.md). **These are the player's and do not change with the module.** |
| ⛔ **Rules of play** | no HP, no dice sizes, no conditions → [`../library/`](../library/) |
| ⛔ **The seed** | the seed is what a module *proposes*, in six fields. **This is what a DM reads while running.** Both exist. |

---

# ⭐ How to write one — the order matters

**Six steps, and doing them out of order produces a persona that reads well and
does nothing.**

| # | | |
|---|---|---|
| 1 | **Read the module's `dm_persona_seed`** | six fields of prose the module *proposes*. ⚠️ **It is a recommendation, not an instruction** — session zero may overrule any of it, and *what gets overruled is data about whether the seed is any good* |
| 2 | **Name the DM, in one sentence** | ⭐ **before any setting.** The name is what makes a register holdable rather than something to remember to perform, and it will do half the work of steps 3 and 4 for free |
| 3 | **Fill the dials — including the empties** | token · clause · evidence. **State `no position` or `no source` on every row you leave open.** Floor is three |
| 4 | **Derive the moves FROM the dials** | ⚠️ **this is the step that gets skipped.** A move invented beside the dials rather than out of them is decoration. Each move should trace to a dial or to the identity — **and one that traces to neither is a founding trait in disguise** |
| 5 | **Write the prediction** | ⭐ **and if you cannot, stop.** A persona with no observable effects has no effects worth claiming, and the honest move is to say so rather than ship it |
| 6 | **Write `wrong for`** | name the modules it fights, **by dial**, so a library is navigable |

> ### ⚠️ Steps 3 and 4 are where a persona is won or lost
>
> **The dial is the POSITION. The move is the BEHAVIOUR.** *"Roll frequency:
> sparse"* tells a DM nothing at eleven at night in round four — **it was never
> meant to.** That is the move's job, and it is why the two layers both exist.

**Prose sections are not one of the six steps.** ⭐ **v1's register, pacing,
lethality, lean-into and tells are all recoverable from dials plus moves** — and
where they were not, **they were mood.**

---

# Part 1 · Identity

**A name and one sentence.** Not a settings block — **something you could
recognise in a room.**

⭐ **Naming the persona is what makes a register holdable rather than something
to remember to perform**, and it makes the swappability legible, which is the
whole argument for this file.

**Plus one line of sensory signature** — which sense this DM reaches for first.
Sounds like decoration; **it is the most recognisable thing a DM has and it costs
nothing.** *(Dial 12 of the taxonomy, folded in here because it is character
rather than a setting.)*

**Record the alternates that were not chosen.** *"Why not that one"* is the
fastest way to understand what a persona is for.

---

# Part 2 · The dials — seven

**A dial is a position on a contested axis.** Set only the ones this persona
takes a real position on. ⭐ **Unset is not a gap — it is the DM's discretion,
which is the half of the job this file exists to protect.**

> ### ⭐ How a dial is filled in — token · clause · evidence
>
> **`<token> — <one clause of why>`**, and where the setting came from.
>
> **The token is a short word from the dial's own axis**, so a library is
> greppable and two personas are comparable. **The clause is the reasoning**,
> which is the half that survives contact with a live table. ⚠️ **Neither
> alone works** — a bare token is a config value nobody can apply, and bare
> prose is v1.
>
> ⭐ **The vocabulary was READ OFF the first retrofit, not authored in
> advance.** Same discipline that produced the module schema and the 42 roles:
> *build one real thing, then say what shape it was.*

### ⛔ An unset row states WHICH KIND of unset

| | |
|---|---|
| **`unset — no position`** | the DM genuinely has no view. ⭐ **Legitimate, and it is discretion rather than a gap** |
| **`unset — no source`** | ⚠️ **nothing upstream proposes it.** Nothing in the module — seed *or* element `constraints` — says anything, so the persona *cannot* set it |
| **`unset — table's`** | ⭐ **it belongs to [`table-agreement.md`](table-agreement.md)** and a persona may not hold it. **Not a gap, and not a break** |

**These look identical on the page and mean three different things.** A DM
declining to have an opinion · **a broken pipeline** · a setting that was never
this file's to make.

> ### ⛔ Before writing `no source`, read the module's element `constraints`
>
> ⚠️ **The seed is not the only upstream.** A module's elements carry
> `constraints` blocks, and they set dials — *"B is a real outcome, not a
> punishment"* is a failure-texture setting sitting in
> `elements/consequences.md`, nowhere near the seed.
>
> **The Registrar's first retrofit marked four rows `no source` by reading only
> the seed. One of them had a source.** ⭐ **`no source` is a claim about the
> whole module, and it is the most consequential thing this file can say** — it
> escalates a task. **Earn it.**

> ⭐ **The distinction is not theoretical.** The Registrar came back with four
> unset rows and **all four are `no source`** — which is how
> `campaigns/modules/README.md` was proven to be still speaking v1 rather than
> merely suspected of it. **SRN-37.**

### The floor — three

**A persona must set at least three dials.** ⚠️ **Fewer and it is not a
persona**, it is a name with a mood attached, and `test-criteria.md` §3c will not
be able to tell it from generically pleasant.

**`no source` rows count against the floor.** ⭐ **If a persona cannot reach
three because the module has no fields, that is a finding about the module** —
do not paper over it by inventing settings it never proposed.

**Clock pressure is TWO rows** — within-session and between-session count
separately, because they are set separately. **A scoped fill** *(a dial pinned
at one moment by a module constraint, open elsewhere)* **does not count.**

> ### ⚠️ The reference sample sits exactly on the floor, and that is a warning
>
> **[The Registrar](../campaigns/modules/a-wild-sheep-chase/DM-persona.md) sets
> three of eight rows. Exactly three.**
>
> ⭐ **A sample teaches its settings, not just its shape** — so the next persona
> built against it will learn that three is normal. **It is not normal. It is
> the minimum, and it is there because the module cannot feed more.**
> **SRN-37.**

---

### ⭐ The stress test — both ends of every dial, filled

**One instance validates the SHAPE. Two opposed instances validate the AXES.**
Fit a format to a single persona and you get a format that only holds that kind
of DM.

**Left: The Registrar** *(the real one)*. **Right: Mave** — a sketch, deliberately
opposite on all seven: warm, loud, generous, improvises constantly.

| dial | The Registrar | Mave |
|---|---|---|
| **Roll frequency** | ⬜ unset — no source | **constant** — the table should feel variance; a story with no dice is a story she wrote alone |
| **Failure texture** | ⬜ unset — no source | **forward** — a miss costs, it does not stop. ⚠️ **She says so out loud in session one** *(the fence)* |
| **Clock pressure** | **constant** — a scene that settles is about to be interrupted | **the world waits** — thinking is free, and she would rather you enjoyed the plan |
| **Humour source** | **situation only** — nobody in the fiction is in on it | **the DM directly** — she is the funniest person at the table and knows it |
| **Silence tolerance** | **lets it sit** — *"he will wait while you decide"* | **fills every pause** — solo silence is dead air, and she will not leave you in it |
| **Canon generation** | ⬜ unset — no source | **rich** — look anywhere and there is a person there with a problem |
| **Callback appetite** | ⬜ unset — no source | **high** — the innkeeper you were rude to in session two is on the council in session nine |

**Result: all seven express both ends.** ⭐ **No dial collapsed into
better-versus-worse under the boundary test**, which is what a fake dial does.

> ### ⭐ The one that looked marginal, and is not
>
> **Canon generation at the `corridor` end** reads like a DM being stingy. It
> is not. **A DM who invents richly every time the player glances sideways
> buries the module's own material** — the adventure someone wrote loses to a
> parade of improvised innkeepers.
>
> **That is a craft position, not scope discipline**, and it is exactly the kind
> of end the boundary test is meant to protect. *(Argued by Imprint,
> 2026-08-26, replacing a weaker defence of my own.)*

⭐ **And note what Mave sets that The Registrar cannot:** exactly the four
`no source` rows. **The dials are expressible; the SEED is the break.** Two
sketches proved that for the price of a table.

---

⚠️ **Most dials are only legible in pairs.** Failure texture plus roll frequency
describes a DM; either alone does not. **Choose by combination, not by taking an
extreme on each axis.**

| # | dial | one end ←→ the other | ⭐ what you would SEE |
|---|---|---|---|
| **1** | **Roll frequency** | narrate past most checks ←→ let the table feel variance | how often dice appear at all. **The strongest single lever on how the game feels** |
| **2** | **Failure texture** | hard failure ←→ succeed-at-cost ←→ fail forward | what happens on a miss. ⚠️ **See the fence below** |
| **3** | **Clock pressure** | the world waits ←→ the world moves while you think | whether deliberating costs anything. **Set within-session and between-session separately** |
| **4** | **Humour source** | situation only ←→ NPCs knowingly ←→ the DM directly ←→ the player alone | **who is allowed to be funny** |
| **5** | **Silence tolerance** | fills every pause ←→ lets it sit | ⭐ **the dial most changed by there being no other players.** Solo silence is much heavier than table silence |
| **6** | **Canon generation rate** | it's a corridor ←→ a rich place appears | how much new world arrives when the player looks somewhere unwritten. **Sets how fast `LIVE/` grows** |
| **7** | **Callback appetite** | let it go ←→ session two's throwaway returns in session nine | ⭐ **the compounding claim as a setting — and the one place Seren can beat a human table, because it does not forget** |

⭐ **Three of these seven — 5, 6, 7 — have no equivalent in published GM
advice**, because nobody had a DM that never forgets and a table of one. **They
are where a Seren persona is genuinely novel rather than an imitation.**

> ### ⚠️ The fence on dial 2
>
> **Fail-forward is not a reversal.** `DM.md`'s interpretation-vs-reversal test
> asks *did the success/failure state change* — and in fail-forward it **did**;
> the cost is what moved. **But it sits next to reversal**, and a persona leaning
> hard into it will read as softening to a player who cannot see the ledger.
>
> **A persona at that end of the dial should say so out loud at the table**,
> once, early. **Undeclared generosity is indistinguishable from cheating.**
>
> ### ⛔ And so dial 2 is the one dial with no `no position`
>
> **Every other dial unset means discretion.** Dial 2 unset means the DM will
> exercise discretion **toward generosity, under pressure** — which is the exact
> risk the fence above describes. ⭐ **The one dial whose default is the
> failure mode cannot be left to default.**
>
> **`unset` on dial 2 means `hard`.** A persona that wants otherwise says so.

⭐ **Dial 4 is what the Registrar's `never` was actually setting.** Naming it as
a dial is what lifts that clause out of Sheep Chase and makes it portable.

---

# Part 3 · Moves — the teeth ⭐

**A dial is descriptive. A move is checkable.**

*"Roll frequency: low"* tells a DM nothing at eleven at night in round four.
***"When the player describes a plan that would obviously work, say what happens
— do not call for a roll"*** does.

> ### A move is a named, triggered, observable thing.
> ### **WHEN <trigger>, <do this>.**

**Three to six per persona.** ⭐ **Every move must carry its trigger**, because a
move with a trigger **needs no external dispatcher** — which is the failure that
has now been caught three times in this repo *(session close, the between-session
clock, and v1's own self-check, all specced as moments with no procedure)*.

**Moves are how a dial becomes behaviour.** Each one should trace to **a dial ·
the identity · or a module element's `constraints`** — and **a move that traces
to none of the three is either a founding trait in disguise or decoration.**

> ### ⚠️ If a move traces to a module constraint, check the dial first
>
> **A module constraint that sets a dial should have set the dial.** A move
> standing on a constraint while its dial reads `unset` is **step 4 run
> backwards**, and it means the dial fill missed a source. ⭐ **The move is not
> wrong — the empty row above it is.**

*(Structure borrowed from Dungeon World's agenda / principles / **moves**, which
treats GM guidance as rules to be altered with the same care as hit points.)*

---

# Part 4 · The prediction ⭐

**One or two sentences, falsifiable, and observable by someone who never read
this file.**

> ### ⭐ The test is not "would a player observe this"
> ### It is: **would this clause DIFFER if you swapped the persona?**
>
> ⚠️ **A clause the module satisfies on its own is inert.** *"Someone will
> insist on procedure while things get worse"* is true because `module.md` says
> a character does that — **it holds under every persona, including generically
> pleasant.**
>
> **Every clause must trace to a dial and flip at the other end of it.** If it
> would still be true under the opposite persona, **it is describing the module,
> not the DM** — and `test-criteria.md` §3c is the one test this file exists to
> pass.

> *If this persona is running, by the second scene you will have heard someone
> interrupted mid-sentence at least twice, and nobody will have made a joke.*

⚠️ **This is the only section that can answer `test-criteria.md` §3c honestly.**
Every other part of a persona can only be judged by someone holding it — **a
prediction can be checked by the player.**

⭐ **And if the prediction cannot be written, that is the finding.** A persona
whose effects are not observable from outside **has no effects worth claiming.**

*(Same discipline as Imprint's calibration prediction bar: a guess that cannot be
predicted from observed behaviour came from a template.)*

---

# Part 5 · When this persona is wrong

**Two or three lines. Every persona is wrong for some module.**

**Name the dial settings that make it a bad fit** — *"a module that needs the
world to wait will fight dial 3"* — so a library is navigable rather than a list
of vibes.

⚠️ **A persona that claims to suit everything is claiming to be generically
pleasant**, which architecture §1 names as one of the two fatal failure modes.

---

# The template

```markdown
# <Name>

<One sentence you could recognise in a room.>
**Reaches first for:** <sense>
*Alternates considered: <name>, <name> — and why not.*

## Dials
| dial | setting |
|---|---|
| Roll frequency | <where, and why> |
| Failure texture | |
| Clock pressure | within-session: · between-session: |
| Humour source | |
| Silence tolerance | |
| Canon generation | |
| Callback appetite | |
<⛔ EVERY ROW STAYS. An open row reads `unset — no position` /
 `unset — no source` / `unset — table's`. Deleting it destroys the
 distinction, which is the most useful thing this format does.>

## Moves
- **When <trigger>,** <do this>.
- **When <trigger>,** <do this>.
- **When <trigger>,** <do this>.

## Prediction
<What a player who never read this file would observe.>

## Wrong for
<The modules this persona fights, named by dial.>
```

**Five parts. No prose sections.** ⚠️ **A dial row is one line.** If a setting
needs a paragraph, the paragraph is a move that has not been written yet.

---

## Provenance

**v1 written 2026-08-26 (SRN-7)**, extracted from
[The Registrar](../campaigns/modules/a-wild-sheep-chase/DM-persona.md).

**v2 the same day**, after Jay's *"it needs more teeth — not for Sheep, for
future,"* against a dial taxonomy drafted with Imprint
*(`seren-dm-persona-dials`, 21 dials across five groups)*.

**Seven of the 21 took a slot. Four moved to the table agreement. One — sensory
bias — folded into identity. Nine were cut**, most because they overlapped
another dial or belonged to the module rather than the DM.

⚠️ **What is a guess, and should be deleted if the play-test says so:**

- **That seven dials is the right number**, and these seven. **Untested.**
- **That moves are the teeth.** Borrowed from a system with a human GM and a full
  table — ⚠️ **Seren has neither**, and no move has ever fired.
- **That a prediction can be written for every persona.** ⭐ **If it cannot, the
  persona is the problem** — but that claim has never been checked.

⛔ **And the standing fact: no persona has ever been loaded by anything.**
`DM.md` carries the adoption clause and is unwritten. **This format is correct,
complete, and inert until SRN-6 lands.**
