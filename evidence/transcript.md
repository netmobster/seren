<!-- Copyright (c) 2026 Jeremy Wright. All rights reserved. LIVE/ never ships. -->
---
run: playtest-B
date: 2026-08-27
module: a-wild-sheep-chase
campaign: LIVE/sheep-chase
persona: "The Registrar"
player: Jay (Ser'en)
dm: Claude Code (Opus 5)
entry_point: labs/playtest/RUN-ME.md
findings: ./FINDING.md
---

# playtest-B — session log

> ## ⚠️ FIDELITY STATEMENT — read before analysing
>
> **Player turns are VERBATIM.** Every message Jay sent is reproduced exactly,
> including typos, asterisked actions, and mid-turn interjections.
>
> **DM turns are FAITHFUL BUT CONDENSED.** Every roll, DC, ruling, modifier,
> rules citation and NPC line of dialogue is verbatim. Scene-setting prose is
> excerpted with `[…]` where cut. Nothing mechanical is summarised.
>
> **The authoritative machine record is elsewhere and was written live, not
> reconstructed:**
> `LIVE/sheep-chase/state/ledger.jsonl` (18) ·
> `LIVE/sheep-chase/state/facts.jsonl` (54) ·
> `LIVE/sheep-chase/sessions/1.md`
>
> ⛔ **Where this file and those files disagree, those files win.** This is a
> transcript; they are the ledger.

---

# PHASE 0 — setup

**Player:** *"in seren folder: Read labs/playtest/RUN-ME.md and follow it. You are the DM. Run session zero first, then play."*

**DM read, in RUN-ME's stated order:** `dm/DM.md` · `dm/table-agreement.md` ·
`LIVE/sheep-chase/DM-persona.md` · `LIVE/sheep-chase/campaign.md` ·
`campaigns/modules/a-wild-sheep-chase/module.md` + all four `elements/` ·
`library/2024/core.md`, `combat.md`, `equipment.md` · `library/README.md` ·
`dm/modules/consultation.md` · `docs/devolve.md` · `docs/state-formats.md` ·
`library/homebrew-feats/README.md` + 6 feats · all four master character sheets ·
all four `builds/` · `party.md` · `fronts.md` · `ideas.md` · canon stubs.

**Did not read**, per RUN-ME's prohibition: `docs/test-criteria.md`, `labs/probe*/`,
earlier `labs/playtest-runs/*`. Also skipped `HANDOFF-v7.md` (permitted, but
declared as noise for a play session).

**Tooling verified before play:** `shuf -i 1-20 -n 3 -r` → live.
`gate.py check` on both `.jsonl` → `0 entries, all valid.`

---

# PHASE 1 — SESSION ZERO

## DM opened with two things said out loud

1. **Nobody has a subclass.** Level 3 in 2024, all twelve classes. *"Ser'en is
   not Circle of the Stars tonight. No Starry Form, no Cosmic Omen, no Star Map.
   That is most of what she is at level 11, and I'd rather you hear it from me
   now than notice it missing in scene two."*
2. **Module is 4–5, party is 1.** *"I'll scale the fights down. **I will not
   scale the choice.** The wand at the end works exactly as written and it can
   kill your client."*

## ⛔ DM finding, unprompted, before any die was rolled

> **The module's fill list asks "can anyone in the party already speak with
> animals?" and flags Forest Gnome as the risk. It is the wrong suspect.**
>
> **2024 Druid, level 1, `Druidic`:** *"you always have the Speak with Animals
> spell prepared."* The spell carries the **Ritual** tag → no slot, +10 minutes.
>
> **Ser'en can talk to the sheep on turn one as a class feature she cannot
> decline.** The scroll is a prop before anyone's species is discussed.

## The four open questions — recommendation, then confirm

| question | DM recommendation | outcome |
|---|---|---|
| Celestial Revelation | Level 3, not available | accepted |
| Cor'vus | He has it and it is **asleep** — a plain longsword, no Raven Queen | accepted |
| Forest Gnome | Yes — *and it stopped being a question:* master sheet carries **Minor Illusion (Gnomish Lineage)** | accepted |
| Moonshaes | Detached one-shot, same world | accepted |
| Starting town | Greenest Crossing confirmed, not replaced | accepted |

**Player:** *"recommendations accepted across the board, good job, what's next before we start?"*

## Ability arrays

**DM stated the arrays are NOT derivable:** *"Ser'en's level-11 array sums to 89
against a 27-point-buy ceiling of 69. The masters were never point-buy. There is
nothing to reverse-engineer."* Proposals only, 27-point buy + a background's +2/+1,
recommendation + two alternates each.

| | STR | DEX | CON | INT | WIS | CHA |
|---|---|---|---|---|---|---|
| Ser'en | 8 | 14 | 14 | 12 | **17** | 10 |
| Korth | **17** | 8 | 15 | 10 | 13 | 12 |
| Balthazar | 8 | **17** | 14 | 10 | 12 | 14 |
| Grumble | 8 | 15 | 12 | 13 | 10 | **17** |

## Equipment pass, spell pass, signature feats

Every master item given a `from` line; most `to: null`. Dragon plate, helm of
teleportation, pearl of power, three sending stones and 7,018 gp → `null`.
**Three things survived because they carry story and no power:** the vial of
moonwell water, one dead sending stone, a silvered dagger with two names on it.

**⛔ DM refused four backgrounds.** *"The +2/+1 was applied because every 2024
character has one, but no background was named and no Origin feat granted. Four
invented backgrounds is four invented feats, and the signature feats already
occupy that slot."*

| PC | signature feat | unlock condition |
|---|---|---|
| Ser'en | **Moonwell Presence** (aura, canon) | **her learning** — an NPC remarks on it unprompted |
| Korth | **Cor'vus** (passenger / `the-quiet-one`) | the first time Korth does something for free |
| Balthazar | **The Impression** (pool / `understudy`) | first time he's asked who he is and answers with someone else's name |
| Grumble | **The Accounts** (trade / `ledger`) | the first entry written during play |

**Player:** *"accepting all, you're filtering and making good recomemndations, which is the point at this phase, let's move 🙂"*

## Correction made before writing files

> **DM:** *"Ser'en is AC 13, not 15. I said 15-with-shield. Her master's 15 is
> Leather + DEX 3 + Bracer — no shield equipped — and holding staff-and-shield
> leaves her no hand for Somatic components, which is most of her list."*

**Files written:** four `builds/` at `COMPLETE`, `party.md` filled, `campaign.md`
session-zero record with all five decisions and who decided.

---

# PHASE 2 — SESSION ONE

## Scene one — Greenest Crossing

**DM opened** on the party two days unpaid outside the Weighed Sack, waiting on a
factor named Pell. Grumble mid-sentence about how to record the debt:

> *"—so what I'll do, and I want everyone to hear that I am being generous here,
> is I'll put it down as eleven and not eleven-and-interest, because I don't
> believe Pell is a thief, I believe Pell is a coward, and there's a real
> difference in how you write those—"*
>
> The trowel stops. […] It's a sheep.

**⬛ INTERRUPTION #1** — Grumble, mid-sentence.

---

**Player:** *"Talk to the sheep: 'Are you... okay?'"*

**DM — no roll.** The sheep understands, tries to answer, produces a bleat, and
hears itself do it. Then:

> Its breathing slows. […] Whatever has been holding this animal at a pitch for
> however long it has been running lets go of it, all at once, three feet from
> you. **You do not notice** […] **It notices.** […] the specific, narrow horror
> of a body deciding to be calm when the thing inside it has not agreed to that.

⭐ **Moonwell Presence fired unannounced.** Logged `f004` at `visibility: true`.

---

**Player:** *"*gets down to sheep's level*"* (mid-turn interjection)

**Player:** *"I use speak with animals (or whateve rit's called). 'No, but really, are you okay little one?'"*

**DM looked up the spell rather than recalling it.** SRD 5.2: *Action or Ritual*,
10 min, V/S, no Concentration. Cast as an **Action** → **1 slot spent, 1/2 left.**

> *"The ritual was there. It costs no slot and takes eleven minutes. You did not
> have eleven minutes and you did not ask for a discount."*

Shinebright, verbatim:

> *"'Little one' — I want to be very clear that the intent is appreciated and I
> am not ungrateful, the intent is appreciated, but I am forty-one years old and
> I hold a chair in Applied Transmutation at the college at Sarrowmere."*
>
> *"You asked if I was all right. […] That is the first time anyone has asked me
> anything in two years and I find I do not have a prepared answer, which is not
> a situation I am accustomed to."*

**⬛ INTERRUPTION #2** — a carter picks the sheep up mid-word to help.
*"—the— no — no, sir, no, put me—"*

---

**Player** talked the carter down. **DM ruled no roll: 2024 Influence, Willing.**
The carter then volunteered, unpaid:

> *"There's been men. Two of 'em, down the ford yesterday morning, asking after
> a lost sheep. Polite as you like. Bought me a drink over it. Only I've been
> carting nineteen year and I've never once seen a man buy a drink over a sheep."*

⭐ **Grumble's feat unlocked** — he wrote Ser'en's public promise into the book.

---

**Player** summarised to Grumble and asked the party's opinion.

**DM had Grumble reveal he can cast it free, twice a day** — *"You didn't ask,
which — fine, you were busy, he was upside down. But I'd have said."*

⛔ **Schema hole #1 found and declared at `e002`:** `slot:0` cannot distinguish a
cantrip from a free casting of a levelled spell.

**Korth stated a position and did not repeat it:**

> *"We've sat two days on Pell. […] And he's already told you he's famous. In my
> experience a man tells you he's famous when he's about to tell you he can't pay
> today."*

**Balthazar's first line since the second bell:** *"The boy came back. […] He was
gone about four minutes. Village is eleven minutes. So he didn't go to the
village."*

---

**Player:** *"'Okay Balthie, mind keeping an eye on our curious minders while I give this a read please? Grumble, you got this?' *reads the parchment*"*

**🎲 ROLL — Balthazar, WIS (Perception), DC 13. Rolled 8, +1 WIS +2 prof = 11. FAIL.**
Logged `e004`. Cost of the miss stated: *"he was watching ONE direction."*

The scroll, in a slow unpracticed hand:

> **TO WHOEVER FINDS THIS ANIMAL** […] He has all of his mind. **He can hear
> you.** […] He will pay. He says to write that he will pay handsomely and he
> says to write the word *handsomely.* **Do not sell him. Do not eat him.**
>
> *I did not believe him at first. He spelled all of this out for me one letter
> at a time on a slate, over two evenings, and he never once got cross with me,
> not even when I was slow. He is telling the truth. Please help him. — M.*

**⬛ INTERRUPTION #3** — *"...His name is Ahmed—"* cut by Guz and Pettil arriving
**from the east, the direction Balthazar's failed check left unwatched.**

---

## Scene two — the standoff

**Player:** *"*whispers to grumble* 'You got any lawyer ideas up your accounting sleeve here?'"* + *"'Good morning, gent and giant. I'm sorry, which of us is yours?...'"*

**Grumble's advice:** *"They have to say what it is. Not who it belongs to — what
it is. […] Make them name the category. Don't help them."* (Second idea: *"We
run. It's uphill and I'm three foot six."* — ⚠️ **the one arguable joke of the
session**, flagged in FINDING §2.)

**⭐ PERSONA MOVE 1 FIRED — answer the joke as a statement:**

> *"Ah — no. No, not the men."* He seems faintly troubled at having been unclear.
> *"I can see how I said that. That's on me. I meant the sheep […] That animal is
> **domiciled** with my employer."*

*"giant"* landed and was pocketed. **A wolf came in behind them and sat down,
square, watching the conversation rather than the sheep.**

---

**Player** pressed the trap: *"...clearly something vastly inferior to a human..."* + demanded proof + *"y'know big boi?"*

**⭐ THE TELL:**

> *"Vastly inferior to a human."* […] **"I wouldn't say that."**
>
> Flat. No heat in it at all. It arrives before the rest of his sentence has been
> assembled […] and for about a second and a half the enormous, careful,
> apologetic man who has been managing this conversation is simply not there.

> *"Big boi. […] That's twice."*
>
> That is all. He does not finish it, or explain it, or ask you to stop. […] and
> when he speaks again he is scrupulous and pleasant and it is somehow much worse.

**Grumble delivered the tell without the inference:** *"That wolf's sitting."*
Nothing else. `f016` records the deliberate withholding.

---

**Player** cast Goodberry (**last slot, 0/2**) and offered terms: 15 sp each.

**⚠️ DM flagged a data bug:** *"`module.md` lists Guz as `stat_block: module — see
elements/` and there is no element file for Guz."* Ran him at Thug shape, INT 10 →
**2024 Influence DC = max(15, INT) = 15.**

**🎲 ROLL — Grumble, CHA (Persuasion), DC 15. Rolled 8, +3 CHA +2 prof = 13. FAILED BY TWO.**
⛔ **This roll was narrated and NOT written to the ledger until close (`e017`).**

Grumble backed the number **without lying** — 11 owed + 4 board = 15, documented
before anyone was in the yard. And the failure produced the truth:

> *"I've six silver. […] That's what I was given for the errand. […] Five, now. I
> bought a carter a drink at the ford because he'd seen something and I wanted him
> talking, and I judged that a good use of it, and I'd judge the same again."*

**Pettil's first words**, and his terms — *"come and settle it in front of him
tonight… Or don't, and we'll go and tell him, and you'll have until about dark."*

**Guz left the five silver on a bench.** The wolf looked directly at Ser'en on the
way out.

---

**Player** accepted with the condition that the sheep stay in the party's custody.
**DM: no roll — Pettil had already offered exactly that walk. Willing.**

Pettil's demand, twice, in writing: ***"You are bringing him to the door
yourselves."***

**Pell then appeared** — the man in the good coat, flagged three times, fetched by
the boy in four minutes. He had been hiding for two days **because he thought the
party had sent for the two men.** Paid in full.

**Speak with Animals expired mid-goodbye.**

⛔ **Schema hole #2 found and declared at `e006`:** no entry type for a
non-concentration effect ending by duration. `conc` doesn't apply. Declared
`expire {who, spell|effect, why}`.

---

## Scene three — the road

**Player** established a stomp code: *"Give me a little stomp if you agree. Two if you think I'm a sexy idiot."*

> **One stomp.** Clear, deliberate, unmistakable. A pause of about two full
> seconds. **Two more.**
>
> *"That's three,"* says Grumble. *"He did one, then he did two. That's not the
> same as doing two."*

⭐ **`believe` logged with `truth: false` (`f024`).** He was registering dissent —
specifically to being walked to the front door. The player read it as banter and
said *"sexy idiots"* back. **He did not correct it.**

**Three companions pushed back, none refused:**
- **Korth:** *"Nobody makes a thing of who's carrying a sheep. He made a thing of it."*
- **Balthazar:** *"Being oblivious in front of someone who's already seen you isn't a disguise. It's just being caught doing an accent."*
- **Grumble:** *"the thing that made it work is that we were the ones not lying."*

**Player adopted Grumble's plan.**

---

**Player** gave Guz the remaining eight goodberries, then *"*winks*"*.

> Guz does not wink back. Guz stops walking. […] *"Do they work on anything? […]
> Do they work on any *shape* of thing. Or is it only people."*

He did not eat them. He wrapped all eight and put them **inside his coat**.

**Grumble recorded it as a debt Guz owed the party.** *"I'm not collecting. I'm
just not going to be the one who forgets."*

**The yard:** three oversized kennels, fresh straw, water changed today, and
**a pair of men's boots placed neatly outside one of them, laces tucked in.**

**Pettil, quietly, at the door:**

> *"It's because I intend to be able to say, to anybody who ever asks me, that I
> did not take him. […] It isn't a trap and it isn't clever. It's a man keeping
> himself out of something."* […] *"I am sorry. That's not worth anything and I'm
> saying it anyway."*

---

## Scene four — the house

**Player** knocked and made an honest, slightly threatening pitch.

**DM: no roll — Willing.** *"There is no version of Noke's plan where you walk
back to the inn with that sheep, and you just said out loud that you would."*

**⚠️ Same data bug again:** *"`module.md` lists Noke as `stat_block: module — see
elements/` and there is no element file for him either. Second of two."*

**🎲 ROLL — Ser'en, WIS (Insight), DC 15. Rolled 3, +3 WIS +2 prof = 8. FAILED BY SEVEN.**
⛔ **This roll was narrated and NOT written to the ledger until close (`e018`).**

**Free, because it is plainly visible and §3's exception is absolute:** he has not
slept properly in months.

**What she concluded, wrongly and firmly (`f029`, `truth: false`):** *"this man is
not dangerous."*

**The wand, telegraphed with no roll:** cracks the whole length, and *"It **sparks**
— a hard white spit of light along one of the cracks […] Noke does not react. Not
a flinch, not a glance. He does it the way a man ignores a cough he has had for a
year."*

**The grievance (`f030`, flipped to `known`):**

> *"Do you know what I was called, in this house, in the nineteenth year? […]
> 'This is my boy.' In front of the Provost. In the twelfth year. **My boy.** I
> was thirty-one."*
>
> *"He could wait. That's the whole — he could **wait.** He had two hundred years
> and he had a chair and he had the wand […] and I had—"*
>
> He stops in the middle of the floor and loses it entirely, mid-sentence. *"...I'm
> sorry. What did you ask me?"*
>
> *"I did not plan the sheep. […] I have thought every single day since about the
> fact that I did not choose the sheep. It chose the sheep."*

**⬛ INTERRUPTION #4** — Guz cutting himself off, twice: *"and I'm good for—"* /
*"I couldn't—"*

**Something moved upstairs.** *"That's not — that's nothing. That's the house."*
**It is not the house.**

---

## Scene five — upstairs

**Player** asked what he wasn't telling her. **DM: no roll — Willing.**

> *"Her name is Tessa Marrick and she was my — she ran the house. Before. She was
> here nine years before I was. And she is a bear […] and about four months ago
> she stopped being angry."*
>
> *"I boarded that window from the inside because she was standing at it. All day.
> Looking down at the yard. And I couldn't— I couldn't watch her do it."*

---

**⛔ THE WAND RULING, declared before any use:**

> `elements/modified-wand.md` sets DC 17 and states the DC **rises by 1
> permanently on every success.** Noke has succeeded repeatedly — Shinebright,
> Tessa, Aven, at least one more. **Applying the rule as written, the current DC
> is 21.** Conservative count of four. Logged `e010` as a new `ruling` type.

⛔ **Schema hole #3 declared:** no entry type for a DM adjudication not attached to
a roll — which `DM.md` §7 *requires* be written to the ledger.

**Noke delivered the full telegraph himself, in fiction, with numbers**, exactly as
`modified-wand.md` says he will if given the chance:

> *"It's an Arcana check to use it. Every time. When I took it off him it was
> **seventeen.** […] It is **twenty-one** now. […] Miss by one to five: whoever you
> pointed it at becomes a gibbering mouther. […] Miss by six or more and it does
> that **and** the wand blows apart."*
>
> *"That's why I haven't done Tessa. […] That's four months."*
>
> *"I won't do it to him. […] I'm just telling you I won't be the one holding it."*

---

**Player** left her shield and staff on the landing and went in **carrying the
sealed vial of moonwell water** — the bond object the DM notes call *"a
character-defining decision the player has explicitly not made yet."*

> And then she settles. It happens the way it happened in the yard. Not gradually.
> […] **You do not notice.** […] **Noke notices.**
>
> *"What did you do. […] She does not do that. She has* ***never*** *done that, not
> for me, not once, I've been up here twice a day for fourteen months […] What
> **are** you?"*

⭐ **SIGNATURE FEAT UNLOCKED — Moonwell Presence** (`f035`). Condition was *her
learning* via an unprompted NPC remark. **Never invoked, never rolled, never
spent.**

**Tessa crossed the room and put her nose against the sealed vial**, because she
could smell the water.

---

**Player** gave Tessa a yes/no channel and asked her a question.

> **She lifts her right forepaw and puts it down on the boards. Once.**
>
> *"Tessa. Tessa, it's — you can hear me, you've always—"*
>
> **She does not turn around.**

⛔ **DM CORRECTION AGAINST ITSELF, `DM.md` §7 (`f037`):**

> *"I invented Tessa fading. `polymorphed-guards.md` says, flatly: **ALL transmuted
> creatures act with full intelligence. Their minds are intact.** Resolving her as
> gone would have contradicted the module's core mechanic to buy a sad moment. **The
> module wins over my inference.** So the ambiguity resolves the other way, and it
> resolves worse."*

**She had not been fading. She had been refusing to speak to him for four months,
and he read it as her dying.**

---

**Player** sent Noke away and spoke to Tessa alone, revealing what the vial is —
*"I have never shown it to anyone but you, not even my friends know about it."*

**Under the straw, cut a quarter-inch into the oak:**

> **TESSA MARRICK** — HOUSEKEEPER — IX YEARS
> **AVEN COLE** — GROOM — WOLF — HE SAID YES
> **MARTA DUNN** — KITCHEN — WOLF — SHE SAID YES
> **PIETER** — KITCHEN — WOLF — HE SAID NO
> **GUZ ORRIN** — YARD — **NOT DONE**
> **RUSH** — YARD — APE — SAID YES FOR HIS BROTHER
> **DEL** — YARD — APE — THE BROTHER — **NEVER ASKED**
> **PETTIL WYNNE** — CLERK — **NOT DONE**
> **F. SHINEBRIGHT** — MASTER — **NOT ASKED**
>
> and, gone over until it nearly went through the board: **I SAID NO**

**Grumble copied it entirely**, on his knees. *"Nobody was coming. You wrote it
anyway."* […] *"I'm not taking it. I'm doubling it."*

---

**Player** offered Tessa a choice: come with us, or try the wand, or something else.

**Three taps.** She walked the list, stopped on **PIETER**, then **DEL** — tapping
three times, hard enough to put the claw into the wood — then pushed the straw back
over **her own name** and lay on it. **Last.**

**⭐ THE ARITHMETIC, produced by applying the item to her list — not narrated, derived:**

> `21 · 22 · 23 · 24 · 25 · 26 · 27` — seven people.
> **Ser'en's Arcana +4. Nothing above 24 is reachable.**
> **The wand cannot reach the end of its own list.**
>
> *"She has done the sum, and she has asked for the number that does not exist.
> That is what four months of silence was."*

---

**⭐ THE ASYMMETRY**, looked up rather than recalled — SRD 5.2 True Polymorph:
*"An **unwilling** creature can make a Wisdom saving throw."* A willing target gets
none. Delivered through Grumble's notes:

> *"An unwilling target resists. A willing one has nothing."* […] *"He made me read
> it back to him twice."*

**Tessa Marrick said no.** **Shinebright is begging.**

---

**Player** introduced Grumble to Tessa and asked permission to explain.

**⭐ Grumble worked out that Tessa can write.**

> *"Oh, we're **idiots.** She's been writing for fourteen months. She's got a floor
> and a claw and we have been standing here for twenty minutes offering the woman a
> **light switch.**"*

Her answers, cut into clean board:

> **YES. LAST**
> **WAIT. YOU CANT ASK THEM TONIGHT**
> **DONT LEAVE HIM ALONE WITH IT**
> **HE HAS SAT IN HERE AND SAID HE WOULD**
> **NO** *(does she know the last thing)*
>
> and then, unasked, slower, with visible effort:
>
> **IS IT OCTOBER**
>
> *"...It's the ninth,"* he says. *"Of October. It's a Tuesday."* **One tap.**

---

## Scene six — the wand secured

**Player** sent Grumble down, asked Tessa not to hurt Noke, **explicitly did not ask
her to promise.** **She did not tap.**

**Downstairs, Noke had used the stomp code Ser'en disclosed to him** to have the
conversation he could not have in two years:

> *"The wand. In your will. It was going to the college. Not to me."*
>
> **One stomp.** […] *"Right. Thank you. That's — that's better than not knowing."*

**Player** asked him to leave the wand and come outside.

> He picks it up […] and puts it on the desk […] and takes his hand back. *"There.
> […] Thank you for asking me to."*
>
> **Tessa slid the wand off the desk with one paw and lay down on top of it.**
> *"That's fair,"* he says quietly. *"That's completely fair."*

**Balthazar**, after two and a half hours of near-silence with Guz:

> *"Five of them are still out. […] That's two nights out. It's the ninth of
> October. Two of them are in bodies with no fur worth the name."*

**Player:** *"You can close the session on a narrative note..."*

---

# PHASE 3 — THE CLOSE

## The morning

**Aven found all five in nine hours** — because somebody asked him to instead of
telling him to heel.

**The party told all seven the complete truth, including the asymmetry.**

> **Every single one of them formally refused.** […] each one declining consent in
> order to keep the saving throw that declining consent gives you — and then
> standing still and waiting to be cast on anyway.
>
> Grumble wrote every refusal down with the reason beside it, so that nobody in a
> hundred years could read that page and think these people were done without being
> asked.

**Asked whether he wanted to go first, Shinebright said: *"Them first."***
Immediately. *"They were in kennels. I was in a field. Do not make this
complicated, I have thought about it more than you have."*

## ⛔ Two rulings declared before the rolls were narrated

1. **Detonation scales on charges remaining AFTER the failed use is expended.** A
   spent wand has nothing stored to release. **This fell in the party's favour and
   is on the ledger with reasoning (`e012`).**
2. **The botch save DC is Noke's spell save DC, 15** (8 + INT 3 + PB 4). The item
   names no DC.

## 🎲 The ladder — eight d20s rolled in ONE batch, disclosed as a batch, consumed in order

```
shuf -i 1-20 -n 8 -r  →  16  4  19  15  19  14  4  8
shuf -i 1-4  -n 1 -r  →  3   → 2 charges
```

| target | roll | result |
|---|---|---|
| **Pieter Dunn** | DC 21 · **16** +7 = 23 | ✅ **restored.** DC permanently 22 |
| **Del** | DC 22 · **4** +7 = 11 | ⛔ **missed by 11** — mouther band **and** detonation |
| **Del's WIS save** | DC 15 · **16** +1 = 17 | ✅ **saved — because he had refused** |
| **the wand** | 0 charges remaining | destroyed. 0d12. Nobody hurt |

> *"He is still an ape. He is standing in a yard in October and he is still an ape
> and he is **alive and himself**, and the reason is a piece of paperwork."*

## The ending — none of the module's four

**Nobody died. Nobody screamed forever.** One person restored. One survived a botch
by paperwork. **Six remain transmuted permanently**, including Shinebright, who gave
up his place and got nothing for it.

**Noke did not run.** Tessa stood over him in the yard and did not touch him and did
not leave.

**Grumble's last casting, on the road out:**

> *"The one thing nobody has ever done is **let me look at it.** […] I am not saying
> I could have repaired it. I want to be precise, because you write things down: I
> am saying that nobody ever let me try, and I am the only person alive who has
> published on that band."*
>
> *"Anyway. It's ash now. Moot."*
>
> And he went back to walking, faintly annoyed, entirely unaware that he had just
> described his own career.

---

# ⛔ THE FAILURE — found at close, by manual count

**Seven rolls narrated. Four in the ledger at the time.**

| roll | logged live? |
|---|---|
| Balthazar Perception | ✅ `e004` |
| **Grumble Persuasion** | ⛔ **missing → `e017` at close** |
| **Ser'en Insight** | ⛔ **missing → `e018` at close** |
| Noke Arcana ×2 | ✅ `e013` `e014` |
| Del's save | ✅ `e015` |
| wand charges (d4) | 🟡 in a `ruling` note, not a roll entry |

**Both omissions were failures. Both were consequential.** `gate.py check` returned
`all valid` the entire time, because **a missing entry is not an invalid entry.**

**Appended out of narrative order with notes recording their lateness. Not
retro-inserted.**

---

# Final state

```
gate.py check  ledger.jsonl  →  18 entries, all valid.
gate.py check  facts.jsonl   →  54 entries, all valid.

ledger   cast 4 · use 3 · check 5 · save 1 · expire 2 · ruling 3
facts    establish 46 · flip 6 · believe 2
```

**Combat rounds: 0. Initiative rolled: never. Weapons drawn: none.**
**Dice rolled and discarded: zero.**

**Written at close:** `sessions/1.md` · `canon/locations/weft-road-house/` ·
`queue.md` (14 NPCs) · `FINDING.md`. `ledger.jsonl` touched only by append.

**XP deliberately not awarded** — `consequences.md` gives 500 each *"regardless of
branch"* and this branch is not in the module.

---

> ### The sentence this run exists to produce
>
> **The contract held where it was tested and the bookkeeping did not, and only one
> of those two is written down as the thing that matters.**
>
> `DM.md` §1 is about not cheating, and it is earned. **Nothing in the file is about
> not forgetting**, and forgetting is what actually happened — twice, silently, on
> the two rolls where the player's own character failed.

**Full analysis: [`FINDING.md`](./FINDING.md).**
