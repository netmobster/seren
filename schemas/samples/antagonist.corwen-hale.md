---
name: "Corwen Hale"
slug: "corwen-hale"
tier: antagonist
axis: vendetta                    # wants the party DESTROYED
role: "antagonist — veteran, inheritor, aggrieved"
species: Human
class: Fighter
subclass: "Battle Master"
level: 3
ruleset: "2024"
proficiency_bonus: 2

grudge: null                      # FILL AT CAMPAIGN CREATION — one line, party-relative
grudge_seed: "He was given a dead man's gear, and the dead man walked past him in the street."
exit: killed
escalation: |
  2 — he has learned how they fight. Brings the counter, not the rematch.
  3 — he stops trying to win the fight and starts trying to take something.
  4+ — he cannot be talked down and he knows it. He says so, which is the last
       honest thing he does.

attaches_to: [jornis-the-forgotten]
fallback: "If Jornis is not in the party — the gear he carries came off SOMEONE
           in the party's past. Every sheet has an item with no story attached
           (architecture §2b, provenance). Use that."

abilities: { str: 16, dex: 12, con: 14, int: 10, wis: 13, cha: 11 }
saves_proficient: [str, con]
skills_proficient: [athletics, intimidation, survival, perception]

ac: 18                            # chain mail 16 + shield
hp: { max: 28, hit_dice: "3d10" }
initiative: 1
speed: { walk: 30 }
passive_perception: 13
languages: [Common]

stat_block: "built — see Actions"
plausible_combat: yes
commands: "three or four men who served with him. They are tired and they are
           still here, which tells you what he is like."
---

<!-- Copyright (c) 2026 Jeremy Wright. All rights reserved. Published for review only; no licence granted. See LICENSE.txt -->

# Corwen Hale

Human Fighter 3, Battle Master. **He is carrying a hero's kit he did not earn,
and the man who earned it threw it away.**

## Voice / Want / Tell

| | |
|---|---|
| **voice** | Flat. Short sentences. No threats — threats are for people hoping not to have to. |
| **want** | For it to have meant something. Failing that, for someone to answer for it. |
| **tell** | **Cleans the weapon while talking to you.** Not menacingly. Devotionally. It is the only thing he owns that matters and he did not buy it. |

The war ended badly. Afterwards a man who had been the reason it did not end
worse gave his gear away in disgust and disappeared under another name. Corwen
got a piece of it. He built twenty years around what that meant.

**Then he found out the man was alive, using a different name, and did not want
to discuss it.** That is the grudge. It is not about the party — it is about one
of them, and the others are in the way.

**`exit: killed`, and it should cost.** He is the one antagonist here with no
good ending, deliberately: one of six should be unresolvable, or the exit field
becomes a promise that everything can be talked through. Killing him should take
something the party wanted to keep — and the interactions log is what makes it
land, because by then they will have several sessions of him being *almost*
reachable.

## Actions

**Extra Attack does not arrive until 5.** At 3 he gets one attack and makes it
count.

| attack | range | hit | damage |
|---|---|---|---|
| **Longsword** *(Sap mastery)* | 5 ft | **+5** | 1d8+3 slashing |
| **Handaxe** *(Vex mastery)* | 20/60 | +5 | 1d6+3 slashing |

**Sap** — on a hit, the target has disadvantage on its next attack roll. He opens
with this on whoever hits hardest, every time, and it is why he survives round
one.

**Superiority Dice** *(4d8, short rest).* **Menacing Attack** *(DC 13 WIS or
Frightened)* · **Trip Attack** *(DC 13 STR or Prone)* · **Riposte** *(reaction,
on a miss against him)*.

**Second Wind** *(2/long rest, 1d10+3).* **Action Surge** *(1/short rest).*

## Equipment

**A weapon that is not his** — the inherited piece. Name it at campaign
creation, not here · chain mail, repaired many times · shield · handaxes x2 · a
token from a unit that no longer exists · no money worth counting

> **Transpose the inherited item, do not invent it.** The master sheet is the
> source of what *kind* of thing it was. Architecture §2b.

## Knows

```yaml
- fact: The name the man used to go by, and what he did under it.
  visibility: true
  note: He will say it aloud at a moment of his choosing. It is his one card.
- fact: How this party fights, from appearance 2 onward.
  visibility: true
  note: Accumulates in the interactions log. That is the mechanism.
- fact: He was given the gear rather than earning it.
  visibility: known
  note: He is not hiding this. He says it first, to control how it is heard.
- fact: The war was lost for reasons that had nothing to do with one man leaving.
  visibility: false
  note: He believes it turned on that. It did not. Never let the DM correct him
        gently — the wrongness IS the character.
```

## Scaling

**At 1-2:** Fighter 1-2, no maneuvers. He loses, and he leaves, and the whole
arc is built on that appearance.
**At 3-5:** as written. Extra Attack at 5 roughly doubles him.
**At 6-8:** Fighter 7-9 — more maneuvers, Know Your Enemy, a +2 weapon. **Give
him Precision Attack here**; it lands the hit that matters.
**At 9-11:** Fighter 11-13, three attacks, Indomitable x2, and **a reputation**.
By this tier he does not have to find the party.
**Cheapest single dial:** the men with him. Corwen alone is a duel. Corwen with
four veterans is a problem, and it costs nothing to add them.

## The interactions log

`LIVE/<campaign>/canon/antagonists/corwen-hale-interactions.md`.

**Log his tactical reads specifically.** Corwen is the antagonist whose
accumulation is *mechanical*: appearance 2 opens with a counter to whatever beat
him in appearance 1. Fought at range? He closes. Concentrated? He goes for the
caster. **Write down what worked, because next time it will not.**

## Provenance

Authored 2026-08-24. Hangs on a character-level fact from the JSON audit: Jornis
the Forgotten carries a discarded name, **Zytharin** — a war hero who gave away
his magic gear in disgust (`characters/ROSTER.md`, audit §1). True about Jornis
in any campaign. **The war itself is deliberately unnamed**; naming it would be
writing a front.
