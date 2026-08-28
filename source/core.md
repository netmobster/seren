<!-- Copyright (c) 2026 Jeremy Wright. All rights reserved. See LICENSE.txt -->

> This work includes material from the System Reference Document 5.2 ("SRD 5.2")
> by Wizards of the Coast LLC, available at https://www.dndbeyond.com/srd. The
> SRD 5.2 is licensed under the Creative Commons Attribution 4.0 International
> License, available at
> https://creativecommons.org/licenses/by/4.0/legalcode.

# Class progression — 2024

**Everything [`../../docs/devolve.md`](../../docs/devolve.md) needs to express a
character at a lower level.** All twelve classes, levels 1–20.

**Built 2026-08-27, SRN-10.** Companion to
[`combat.md`](combat.md); the raw corpus is
[`../srd-5.2/`](../srd-5.2/).

> ## ⭐ THIS FILE IS MECHANICAL. The rules are here; the judgement is not.
>
> **What a level-5 version of a character KNOWS is a table lookup.** What they
> **carry**, and which spells they **prepared**, is not — that is
> [`devolve.md`](../../docs/devolve.md) §4, and it is a conversation.

---

# ⛔ Two things this project believed that are wrong

**Both were stated in `architecture.md` §2b and repeated downstream. Both are
2014 facts carried into a 2024 project.**

## 1. ASIs are at 4 / 8 / 12 / 16 — **not 19**

**Level 19 is `Epic Boon`, which is a different thing.** And ⚠️ **"fixed" is
wrong too — three classes get extra ones:**

| | |
|---|---|
| **Nine classes** | 4 · 8 · 12 · 16 |
| **Fighter** | 4 · **6** · 8 · 12 · **14** · 16 |
| **Rogue** | 4 · 8 · **10** · 12 · 16 |

⛔ **A devolve that dropped an ASI at 19 and missed Fighter's at 6 would produce
a build that is wrong in both directions and legal-looking in neither.**

## 2. Subclass FEATURES are not at 3 / 6 / 10 / 14

⭐ **The subclass itself is gained at level 3 by all twelve** — that part was
right. **When its features arrive is per-class and varies a lot:**

| class | subclass feature levels |
|---|---|
| Barbarian · Druid · Warlock · Wizard | 6 · 10 · 14 |
| Bard · Sorcerer | 6 · 14 *(Sorcerer also 18)* |
| Cleric | **6 · 17** |
| Monk | 6 · 11 · 17 |
| Fighter | **7 · 10 · 15 · 18** |
| Paladin | **7 · 15 · 20** |
| Ranger | 7 · 11 · 15 |
| Rogue | **9 · 13 · 17** |

**Only four of twelve match the number that was written down.**

---

# ⭐ How these tables were extracted, and why the first attempt would have lied

**`srd-5.2-raw.txt` was made with `pdftotext -layout`.** On the SRD's
**two-column pages that interleaves the columns**, and the class tables come out
with holes:

```
Level  Proficiency  Class Features              Cantrips  Prepared   ——Spell Slots——
  1    Bonus        Spellcasting, Ritual Adept,     3       Spells   123456789
                    Arcane Recovery                                  2 ————————
  2         +2      Scholar                                     4
  3                 Wizard Subclass
```

⛔ **Level 1 has no proficiency bonus. Level 2 has no cantrip count. Level 3 is
empty.** ⚠️ **A careful reader fills those gaps from memory and produces a table
that looks complete and is silently wrong** — which is exactly how `Thug` was
recorded as *"cut from SRD 5.2"* in four documents when the 2024 name is
**`Tough`**.

**`pdftotext -raw` reads in content order and the rows come out whole.** Saved
alongside as [`../srd-5.2/srd-5.2-reading-order.txt`](../srd-5.2/srd-5.2-reading-order.txt).

> ### ⭐ The fix was a flag, not a reconstruction. Nothing here was typed from memory.

## What was checked, against what

| check | cells | |
|---|---|---|
| **Proficiency bonus** `== 2 + ⌊(level−1)/4⌋` | **240** | ✅ |
| **Five full casters share ONE slot progression** *(Bard · Cleric · Druid · Sorcerer · Wizard)* | **900** | ✅ |
| **Paladin's slots == Ranger's** | **100** | ✅ |
| **20 rows per class, uniform column count** | 12 classes | ✅ |

⭐ **1,240 cells cross-checked against an invariant rather than eyeballed.** Two
parse faults surfaced *because* a check failed, and both were real data the
parser was eating: **`—` as the feature name on levels with no feature**, and
**Bard's `D6` Bardic Die** *(capital D, no leading digit)*.

⚠️ **What is NOT verified:** the feature NAMES in each row are transcribed, not
checked against the class descriptions. **A misspelled feature is possible; a
wrong number is not.**

---

# The universal table

**Proficiency bonus applies to every class.** ⭐ **It is a pure function of
level** — `2 + ⌊(level−1)/4⌋` — verified against all 240 cells, so a devolve
never needs to look it up.

| level | 1–4 | 5–8 | 9–12 | 13–16 | 17–20 |
|---|---|---|---|---|---|
| **bonus** | +2 | +3 | +4 | +5 | +6 |

---

# The class tables

## Barbarian

| Level | PB | Class Features | Rages | Rage Damage | Weapon Mastery |
|---|---|---|---|---|---|
| 1 | +2 | Rage, Unarmored Defense, Weapon Mastery | 2 | +2 | 2 |
| 2 | +2 | Danger Sense, Reckless Attack | 2 | +2 | 2 |
| 3 | +2 | Barbarian Subclass, Primal Knowledge | 3 | +2 | 2 |
| 4 | +2 | Ability Score Improvement | 3 | +2 | 3 |
| 5 | +3 | Extra Attack, Fast Movement | 3 | +2 | 3 |
| 6 | +3 | Subclass feature | 4 | +2 | 3 |
| 7 | +3 | Feral Instinct, Instinctive Pounce | 4 | +2 | 3 |
| 8 | +3 | Ability Score Improvement | 4 | +2 | 3 |
| 9 | +4 | Brutal Strike | 4 | +3 | 3 |
| 10 | +4 | Subclass feature | 4 | +3 | 4 |
| 11 | +4 | Relentless Rage | 4 | +3 | 4 |
| 12 | +4 | Ability Score Improvement | 5 | +3 | 4 |
| 13 | +5 | Improved Brutal Strike | 5 | +3 | 4 |
| 14 | +5 | Subclass feature | 5 | +3 | 4 |
| 15 | +5 | Persistent Rage | 5 | +3 | 4 |
| 16 | +5 | Ability Score Improvement | 5 | +4 | 4 |
| 17 | +6 | Improved Brutal Strike | 6 | +4 | 4 |
| 18 | +6 | Indomitable Might | 6 | +4 | 4 |
| 19 | +6 | Epic Boon | 6 | +4 | 4 |
| 20 | +6 | Primal Champion | 6 | +4 | 4 |

## Bard

| Level | PB | Class Features | Bardic Die | Cantrips | Prepared | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | +2 | Bardic Inspiration, Spellcasting | D6 | 2 | 4 | 2 | — | — | — | — | — | — | — | — |
| 2 | +2 | Expertise, Jack of All Trades | D6 | 2 | 5 | 3 | — | — | — | — | — | — | — | — |
| 3 | +2 | Bard Subclass | D6 | 2 | 6 | 4 | 2 | — | — | — | — | — | — | — |
| 4 | +2 | Ability Score Improvement | D6 | 3 | 7 | 4 | 3 | — | — | — | — | — | — | — |
| 5 | +3 | Font of Inspiration | D8 | 3 | 9 | 4 | 3 | 2 | — | — | — | — | — | — |
| 6 | +3 | Subclass feature | D8 | 3 | 10 | 4 | 3 | 3 | — | — | — | — | — | — |
| 7 | +3 | Countercharm | D8 | 3 | 11 | 4 | 3 | 3 | 1 | — | — | — | — | — |
| 8 | +3 | Ability Score Improvement | D8 | 3 | 12 | 4 | 3 | 3 | 2 | — | — | — | — | — |
| 9 | +4 | Expertise | D8 | 3 | 14 | 4 | 3 | 3 | 3 | 1 | — | — | — | — |
| 10 | +4 | Magical Secrets | D10 | 4 | 15 | 4 | 3 | 3 | 3 | 2 | — | — | — | — |
| 11 | +4 | — | D10 | 4 | 16 | 4 | 3 | 3 | 3 | 2 | 1 | — | — | — |
| 12 | +4 | Ability Score Improvement | D10 | 4 | 16 | 4 | 3 | 3 | 3 | 2 | 1 | — | — | — |
| 13 | +5 | — | D10 | 4 | 17 | 4 | 3 | 3 | 3 | 2 | 1 | 1 | — | — |
| 14 | +5 | Subclass feature | D10 | 4 | 17 | 4 | 3 | 3 | 3 | 2 | 1 | 1 | — | — |
| 15 | +5 | — | D12 | 4 | 18 | 4 | 3 | 3 | 3 | 2 | 1 | 1 | 1 | — |
| 16 | +5 | Ability Score Improvement | D12 | 4 | 18 | 4 | 3 | 3 | 3 | 2 | 1 | 1 | 1 | — |
| 17 | +6 | — | D12 | 4 | 19 | 4 | 3 | 3 | 3 | 2 | 1 | 1 | 1 | 1 |
| 18 | +6 | Superior Inspiration | D12 | 4 | 20 | 4 | 3 | 3 | 3 | 3 | 1 | 1 | 1 | 1 |
| 19 | +6 | Epic Boon | D12 | 4 | 21 | 4 | 3 | 3 | 3 | 3 | 2 | 1 | 1 | 1 |
| 20 | +6 | Words of Creation | D12 | 4 | 22 | 4 | 3 | 3 | 3 | 3 | 2 | 2 | 1 | 1 |

## Cleric

| Level | PB | Class Features | Channel Divinity | Cantrips | Prepared | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | +2 | Spellcasting, Divine Order | — | 3 | 4 | 2 | — | — | — | — | — | — | — | — |
| 2 | +2 | Channel Divinity | 2 | 3 | 5 | 3 | — | — | — | — | — | — | — | — |
| 3 | +2 | Cleric Subclass | 2 | 3 | 6 | 4 | 2 | — | — | — | — | — | — | — |
| 4 | +2 | Ability Score Improvement | 2 | 4 | 7 | 4 | 3 | — | — | — | — | — | — | — |
| 5 | +3 | Sear Undead | 2 | 4 | 9 | 4 | 3 | 2 | — | — | — | — | — | — |
| 6 | +3 | Subclass feature | 3 | 4 | 10 | 4 | 3 | 3 | — | — | — | — | — | — |
| 7 | +3 | Blessed Strikes | 3 | 4 | 11 | 4 | 3 | 3 | 1 | — | — | — | — | — |
| 8 | +3 | Ability Score Improvement | 3 | 4 | 12 | 4 | 3 | 3 | 2 | — | — | — | — | — |
| 9 | +4 | — | 3 | 4 | 14 | 4 | 3 | 3 | 3 | 1 | — | — | — | — |
| 10 | +4 | Divine Intervention | 3 | 5 | 15 | 4 | 3 | 3 | 3 | 2 | — | — | — | — |
| 11 | +4 | — | 3 | 5 | 16 | 4 | 3 | 3 | 3 | 2 | 1 | — | — | — |
| 12 | +4 | Ability Score Improvement | 3 | 5 | 16 | 4 | 3 | 3 | 3 | 2 | 1 | — | — | — |
| 13 | +5 | — | 3 | 5 | 17 | 4 | 3 | 3 | 3 | 2 | 1 | 1 | — | — |
| 14 | +5 | Improved Blessed Strikes | 3 | 5 | 17 | 4 | 3 | 3 | 3 | 2 | 1 | 1 | — | — |
| 15 | +5 | — | 3 | 5 | 18 | 4 | 3 | 3 | 3 | 2 | 1 | 1 | 1 | — |
| 16 | +5 | Ability Score Improvement | 3 | 5 | 18 | 4 | 3 | 3 | 3 | 2 | 1 | 1 | 1 | — |
| 17 | +6 | Subclass feature | 3 | 5 | 19 | 4 | 3 | 3 | 3 | 2 | 1 | 1 | 1 | 1 |
| 18 | +6 | — | 4 | 5 | 20 | 4 | 3 | 3 | 3 | 3 | 1 | 1 | 1 | 1 |
| 19 | +6 | Epic Boon | 4 | 5 | 21 | 4 | 3 | 3 | 3 | 3 | 2 | 1 | 1 | 1 |
| 20 | +6 | Greater Divine Intervention | 4 | 5 | 22 | 4 | 3 | 3 | 3 | 3 | 2 | 2 | 1 | 1 |

## Druid

| Level | PB | Class Features | Wild Shape | Cantrips | Prepared | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | +2 | Spellcasting, Druidic, Primal Order | — | 2 | 4 | 2 | — | — | — | — | — | — | — | — |
| 2 | +2 | Wild Shape, Wild Companion | 2 | 2 | 5 | 3 | — | — | — | — | — | — | — | — |
| 3 | +2 | Druid Subclass | 2 | 2 | 6 | 4 | 2 | — | — | — | — | — | — | — |
| 4 | +2 | Ability Score Improvement | 2 | 3 | 7 | 4 | 3 | — | — | — | — | — | — | — |
| 5 | +3 | Wild Resurgence | 2 | 3 | 9 | 4 | 3 | 2 | — | — | — | — | — | — |
| 6 | +3 | Subclass feature | 3 | 3 | 10 | 4 | 3 | 3 | — | — | — | — | — | — |
| 7 | +3 | Elemental Fury | 3 | 3 | 11 | 4 | 3 | 3 | 1 | — | — | — | — | — |
| 8 | +3 | Ability Score Improvement | 3 | 3 | 12 | 4 | 3 | 3 | 2 | — | — | — | — | — |
| 9 | +4 | — | 3 | 3 | 14 | 4 | 3 | 3 | 3 | 1 | — | — | — | — |
| 10 | +4 | Subclass feature | 3 | 4 | 15 | 4 | 3 | 3 | 3 | 2 | — | — | — | — |
| 11 | +4 | — | 3 | 4 | 16 | 4 | 3 | 3 | 3 | 2 | 1 | — | — | — |
| 12 | +4 | Ability Score Improvement | 3 | 4 | 16 | 4 | 3 | 3 | 3 | 2 | 1 | — | — | — |
| 13 | +5 | — | 3 | 4 | 17 | 4 | 3 | 3 | 3 | 2 | 1 | 1 | — | — |
| 14 | +5 | Subclass feature | 3 | 4 | 17 | 4 | 3 | 3 | 3 | 2 | 1 | 1 | — | — |
| 15 | +5 | Improved Elemental Fury | 3 | 4 | 18 | 4 | 3 | 3 | 3 | 2 | 1 | 1 | 1 | — |
| 16 | +5 | Ability Score Improvement | 3 | 4 | 18 | 4 | 3 | 3 | 3 | 2 | 1 | 1 | 1 | — |
| 17 | +6 | — | 4 | 4 | 19 | 4 | 3 | 3 | 3 | 2 | 1 | 1 | 1 | 1 |
| 18 | +6 | Beast Spells | 4 | 4 | 20 | 4 | 3 | 3 | 3 | 3 | 1 | 1 | 1 | 1 |
| 19 | +6 | Epic Boon | 4 | 4 | 21 | 4 | 3 | 3 | 3 | 3 | 2 | 1 | 1 | 1 |
| 20 | +6 | Archdruid | 4 | 4 | 22 | 4 | 3 | 3 | 3 | 3 | 2 | 2 | 1 | 1 |

## Fighter

| Level | PB | Class Features | Second Wind | Weapon Mastery |
|---|---|---|---|---|
| 1 | +2 | Fighting Style, Second Wind, Weapon Mastery | 2 | 3 |
| 2 | +2 | Action Surge (one use), Tactical Mind | 2 | 3 |
| 3 | +2 | Fighter Subclass | 2 | 3 |
| 4 | +2 | Ability Score Improvement | 3 | 4 |
| 5 | +3 | Extra Attack, Tactical Shift | 3 | 4 |
| 6 | +3 | Ability Score Improvement | 3 | 4 |
| 7 | +3 | Subclass feature | 3 | 4 |
| 8 | +3 | Ability Score Improvement | 3 | 4 |
| 9 | +4 | Indomitable (one use), Tactical Master | 3 | 4 |
| 10 | +4 | Subclass feature | 4 | 5 |
| 11 | +4 | Two Extra Attacks | 4 | 5 |
| 12 | +4 | Ability Score Improvement | 4 | 5 |
| 13 | +5 | Indomitable (two uses), Studied Attacks | 4 | 5 |
| 14 | +5 | Ability Score Improvement | 4 | 5 |
| 15 | +5 | Subclass feature | 4 | 5 |
| 16 | +5 | Ability Score Improvement | 4 | 6 |
| 17 | +6 | Action Surge (two uses), Indomitable (three uses) | 4 | 6 |
| 18 | +6 | Subclass feature | 4 | 6 |
| 19 | +6 | Epic Boon | 4 | 6 |
| 20 | +6 | Three Extra Attacks | 4 | 6 |

## Monk

| Level | PB | Class Features | Martial Arts | Focus Points | Unarmored Movement |
|---|---|---|---|---|---|
| 1 | +2 | Martial Arts, Unarmored Defense | 1d6 | — | — |
| 2 | +2 | Monk’s Focus, Unarmored Movement, Uncanny Metabolism | 1d6 | 2 | +10ft. |
| 3 | +2 | Deflect Attacks, Monk Subclass | 1d6 | 3 | +10ft. |
| 4 | +2 | Ability Score Improvement, Slow Fall | 1d6 | 4 | +10ft. |
| 5 | +3 | Extra Attack, Stunning Strike | 1d8 | 5 | +10ft. |
| 6 | +3 | Empowered Strikes, Subclass feature | 1d8 | 6 | +15ft. |
| 7 | +3 | Evasion | 1d8 | 7 | +15ft. |
| 8 | +3 | Ability Score Improvement | 1d8 | 8 | +15ft. |
| 9 | +4 | Acrobatic Movement | 1d8 | 9 | +15ft. |
| 10 | +4 | Heightened Focus, Self-Restoration | 1d8 | 10 | +20ft. |
| 11 | +4 | Subclass feature | 1d10 | 11 | +20ft. |
| 12 | +4 | Ability Score Improvement | 1d10 | 12 | +20ft. |
| 13 | +5 | Deflect Energy | 1d10 | 13 | +20ft. |
| 14 | +5 | Disciplined Survivor | 1d10 | 14 | +25ft. |
| 15 | +5 | Perfect Focus | 1d10 | 15 | +25ft. |
| 16 | +5 | Ability Score Improvement | 1d10 | 16 | +25ft. |
| 17 | +6 | Subclass feature | 1d12 | 17 | +25ft. |
| 18 | +6 | Superior Defense | 1d12 | 18 | +30ft. |
| 19 | +6 | Epic Boon | 1d12 | 19 | +30ft. |
| 20 | +6 | Body and Mind | 1d12 | 20 | +30ft. |

## Paladin

| Level | PB | Class Features | Channel Divinity | Prepared | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|---|---|---|---|
| 1 | +2 | Lay On Hands, Spellcasting, Weapon Mastery | — | 2 | 2 | — | — | — | — |
| 2 | +2 | Fighting Style, Paladin’s Smite | — | 3 | 2 | — | — | — | — |
| 3 | +2 | Channel Divinity, Paladin Subclass | 2 | 4 | 3 | — | — | — | — |
| 4 | +2 | Ability Score Improvement | 2 | 5 | 3 | — | — | — | — |
| 5 | +3 | Extra Attack, Faithful Steed | 2 | 6 | 4 | 2 | — | — | — |
| 6 | +3 | Aura of Protection | 2 | 6 | 4 | 2 | — | — | — |
| 7 | +3 | Subclass feature | 2 | 7 | 4 | 3 | — | — | — |
| 8 | +3 | Ability Score Improvement | 2 | 7 | 4 | 3 | — | — | — |
| 9 | +4 | Abjure Foes | 2 | 9 | 4 | 3 | 2 | — | — |
| 10 | +4 | Aura of Courage | 2 | 9 | 4 | 3 | 2 | — | — |
| 11 | +4 | Radiant Strikes | 3 | 10 | 4 | 3 | 3 | — | — |
| 12 | +4 | Ability Score Improvement | 3 | 10 | 4 | 3 | 3 | — | — |
| 13 | +5 | — | 3 | 11 | 4 | 3 | 3 | 1 | — |
| 14 | +5 | Restoring Touch | 3 | 11 | 4 | 3 | 3 | 1 | — |
| 15 | +5 | Subclass feature | 3 | 12 | 4 | 3 | 3 | 2 | — |
| 16 | +5 | Ability Score Improvement | 3 | 12 | 4 | 3 | 3 | 2 | — |
| 17 | +6 | — | 3 | 14 | 4 | 3 | 3 | 3 | 1 |
| 18 | +6 | Aura Expansion | 3 | 14 | 4 | 3 | 3 | 3 | 1 |
| 19 | +6 | Epic Boon | 3 | 15 | 4 | 3 | 3 | 3 | 2 |
| 20 | +6 | Subclass feature | 3 | 15 | 4 | 3 | 3 | 3 | 2 |

## Ranger

| Level | PB | Class Features | Favored Enemy | Prepared | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|---|---|---|---|
| 1 | +2 | Spellcasting, Favored Enemy, Weapon Mastery | 2 | 2 | 2 | — | — | — | — |
| 2 | +2 | Deft Explorer, Fighting Style | 2 | 3 | 2 | — | — | — | — |
| 3 | +2 | Ranger Subclass | 2 | 4 | 3 | — | — | — | — |
| 4 | +2 | Ability Score Improvement | 2 | 5 | 3 | — | — | — | — |
| 5 | +3 | Extra Attack | 3 | 6 | 4 | 2 | — | — | — |
| 6 | +3 | Roving | 3 | 6 | 4 | 2 | — | — | — |
| 7 | +3 | Subclass feature | 3 | 7 | 4 | 3 | — | — | — |
| 8 | +3 | Ability Score Improvement | 3 | 7 | 4 | 3 | — | — | — |
| 9 | +4 | Expertise | 4 | 9 | 4 | 3 | 2 | — | — |
| 10 | +4 | Tireless | 4 | 9 | 4 | 3 | 2 | — | — |
| 11 | +4 | Subclass feature | 4 | 10 | 4 | 3 | 3 | — | — |
| 12 | +4 | Ability Score Improvement | 4 | 10 | 4 | 3 | 3 | — | — |
| 13 | +5 | Relentless Hunter | 5 | 11 | 4 | 3 | 3 | 1 | — |
| 14 | +5 | Nature’s Veil | 5 | 11 | 4 | 3 | 3 | 1 | — |
| 15 | +5 | Subclass feature | 5 | 12 | 4 | 3 | 3 | 2 | — |
| 16 | +5 | Ability Score Improvement | 5 | 12 | 4 | 3 | 3 | 2 | — |
| 17 | +6 | Precise Hunter | 6 | 14 | 4 | 3 | 3 | 3 | 1 |
| 18 | +6 | Feral Senses | 6 | 14 | 4 | 3 | 3 | 3 | 1 |
| 19 | +6 | Epic Boon | 6 | 15 | 4 | 3 | 3 | 3 | 2 |
| 20 | +6 | Foe Slayer | 6 | 15 | 4 | 3 | 3 | 3 | 2 |

## Rogue

| Level | PB | Class Features | Sneak Attack |
|---|---|---|---|
| 1 | +2 | Expertise, Sneak Attack, Thieves’ Cant, Weapon Mastery | 1d6 |
| 2 | +2 | Cunning Action | 1d6 |
| 3 | +2 | Rogue Subclass, Steady Aim | 2d6 |
| 4 | +2 | Ability Score Improvement | 2d6 |
| 5 | +3 | Cunning Strike, Uncanny Dodge | 3d6 |
| 6 | +3 | Expertise | 3d6 |
| 7 | +3 | Evasion, Reliable Talent | 4d6 |
| 8 | +3 | Ability Score Improvement | 4d6 |
| 9 | +4 | Subclass feature | 5d6 |
| 10 | +4 | Ability Score Improvement | 5d6 |
| 11 | +4 | Improved Cunning Strike | 6d6 |
| 12 | +4 | Ability Score Improvement | 6d6 |
| 13 | +5 | Subclass feature | 7d6 |
| 14 | +5 | Devious Strikes | 7d6 |
| 15 | +5 | Slippery Mind | 8d6 |
| 16 | +5 | Ability Score Improvement | 8d6 |
| 17 | +6 | Subclass feature | 9d6 |
| 18 | +6 | Elusive | 9d6 |
| 19 | +6 | Epic Boon | 10d6 |
| 20 | +6 | Stroke of Luck | 10d6 |

## Sorcerer

| Level | PB | Class Features | Sorcery Points | Cantrips | Prepared | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | +2 | Spellcasting, Innate Sorcery | — | 4 | 2 | 2 | — | — | — | — | — | — | — | — |
| 2 | +2 | Font of Magic, Metamagic | 2 | 4 | 4 | 3 | — | — | — | — | — | — | — | — |
| 3 | +2 | Sorcerer Subclass | 3 | 4 | 6 | 4 | 2 | — | — | — | — | — | — | — |
| 4 | +2 | Ability Score Improvement | 4 | 5 | 7 | 4 | 3 | — | — | — | — | — | — | — |
| 5 | +3 | Sorcerous Restoration | 5 | 5 | 9 | 4 | 3 | 2 | — | — | — | — | — | — |
| 6 | +3 | Subclass feature | 6 | 5 | 10 | 4 | 3 | 3 | — | — | — | — | — | — |
| 7 | +3 | Sorcery Incarnate | 7 | 5 | 11 | 4 | 3 | 3 | 1 | — | — | — | — | — |
| 8 | +3 | Ability Score Improvement | 8 | 5 | 12 | 4 | 3 | 3 | 2 | — | — | — | — | — |
| 9 | +4 | — | 9 | 5 | 14 | 4 | 3 | 3 | 3 | 1 | — | — | — | — |
| 10 | +4 | Metamagic | 10 | 6 | 15 | 4 | 3 | 3 | 3 | 2 | — | — | — | — |
| 11 | +4 | — | 11 | 6 | 16 | 4 | 3 | 3 | 3 | 2 | 1 | — | — | — |
| 12 | +4 | Ability Score Improvement | 12 | 6 | 16 | 4 | 3 | 3 | 3 | 2 | 1 | — | — | — |
| 13 | +5 | — | 13 | 6 | 17 | 4 | 3 | 3 | 3 | 2 | 1 | 1 | — | — |
| 14 | +5 | Subclass feature | 14 | 6 | 17 | 4 | 3 | 3 | 3 | 2 | 1 | 1 | — | — |
| 15 | +5 | — | 15 | 6 | 18 | 4 | 3 | 3 | 3 | 2 | 1 | 1 | 1 | — |
| 16 | +5 | Ability Score Improvement | 16 | 6 | 18 | 4 | 3 | 3 | 3 | 2 | 1 | 1 | 1 | — |
| 17 | +6 | Metamagic | 17 | 6 | 19 | 4 | 3 | 3 | 3 | 2 | 1 | 1 | 1 | 1 |
| 18 | +6 | Subclass feature | 18 | 6 | 20 | 4 | 3 | 3 | 3 | 3 | 1 | 1 | 1 | 1 |
| 19 | +6 | Epic Boon | 19 | 6 | 21 | 4 | 3 | 3 | 3 | 3 | 2 | 1 | 1 | 1 |
| 20 | +6 | Arcane Apotheosis | 20 | 6 | 22 | 4 | 3 | 3 | 3 | 3 | 2 | 2 | 1 | 1 |

## Warlock

| Level | PB | Class Features | Invocations | Cantrips | Prepared | Spell Slots | Slot Level |
|---|---|---|---|---|---|---|---|
| 1 | +2 | Eldritch Invocations, Pact Magic | 1 | 2 | 2 | 1 | 1 |
| 2 | +2 | Magical Cunning | 3 | 2 | 3 | 2 | 1 |
| 3 | +2 | Warlock Subclass | 3 | 2 | 4 | 2 | 2 |
| 4 | +2 | Ability Score Improvement | 3 | 3 | 5 | 2 | 2 |
| 5 | +3 | — | 5 | 3 | 6 | 2 | 3 |
| 6 | +3 | Subclass feature | 5 | 3 | 7 | 2 | 3 |
| 7 | +3 | — | 6 | 3 | 8 | 2 | 4 |
| 8 | +3 | Ability Score Improvement | 6 | 3 | 9 | 2 | 4 |
| 9 | +4 | Contact Patron | 7 | 3 | 10 | 2 | 5 |
| 10 | +4 | Subclass feature | 7 | 4 | 10 | 2 | 5 |
| 11 | +4 | Mystic Arcanum (level 6 spell) | 7 | 4 | 11 | 3 | 5 |
| 12 | +4 | Ability Score Improvement | 8 | 4 | 11 | 3 | 5 |
| 13 | +5 | Mystic Arcanum (level 7 spell) | 8 | 4 | 12 | 3 | 5 |
| 14 | +5 | Subclass feature | 8 | 4 | 12 | 3 | 5 |
| 15 | +5 | Mystic Arcanum (level 8 spell) | 9 | 4 | 13 | 3 | 5 |
| 16 | +5 | Ability Score Improvement | 9 | 4 | 13 | 3 | 5 |
| 17 | +6 | Mystic Arcanum (level 9 spell) | 9 | 4 | 14 | 4 | 5 |
| 18 | +6 | — | 10 | 4 | 14 | 4 | 5 |
| 19 | +6 | Epic Boon | 10 | 4 | 15 | 4 | 5 |
| 20 | +6 | Eldritch Master | 10 | 4 | 15 | 4 | 5 |

## Wizard

| Level | PB | Class Features | Cantrips | Prepared | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | +2 | Spellcasting, Ritual Adept, Arcane Recovery | 3 | 4 | 2 | — | — | — | — | — | — | — | — |
| 2 | +2 | Scholar | 3 | 5 | 3 | — | — | — | — | — | — | — | — |
| 3 | +2 | Wizard Subclass | 3 | 6 | 4 | 2 | — | — | — | — | — | — | — |
| 4 | +2 | Ability Score Improvement | 4 | 7 | 4 | 3 | — | — | — | — | — | — | — |
| 5 | +3 | Memorize Spell | 4 | 9 | 4 | 3 | 2 | — | — | — | — | — | — |
| 6 | +3 | Subclass feature | 4 | 10 | 4 | 3 | 3 | — | — | — | — | — | — |
| 7 | +3 | — | 4 | 11 | 4 | 3 | 3 | 1 | — | — | — | — | — |
| 8 | +3 | Ability Score Improvement | 4 | 12 | 4 | 3 | 3 | 2 | — | — | — | — | — |
| 9 | +4 | — | 4 | 14 | 4 | 3 | 3 | 3 | 1 | — | — | — | — |
| 10 | +4 | Subclass feature | 5 | 15 | 4 | 3 | 3 | 3 | 2 | — | — | — | — |
| 11 | +4 | — | 5 | 16 | 4 | 3 | 3 | 3 | 2 | 1 | — | — | — |
| 12 | +4 | Ability Score Improvement | 5 | 16 | 4 | 3 | 3 | 3 | 2 | 1 | — | — | — |
| 13 | +5 | — | 5 | 17 | 4 | 3 | 3 | 3 | 2 | 1 | 1 | — | — |
| 14 | +5 | Subclass feature | 5 | 18 | 4 | 3 | 3 | 3 | 2 | 1 | 1 | — | — |
| 15 | +5 | — | 5 | 19 | 4 | 3 | 3 | 3 | 2 | 1 | 1 | 1 | — |
| 16 | +5 | Ability Score Improvement | 5 | 21 | 4 | 3 | 3 | 3 | 2 | 1 | 1 | 1 | — |
| 17 | +6 | — | 5 | 22 | 4 | 3 | 3 | 3 | 2 | 1 | 1 | 1 | 1 |
| 18 | +6 | Spell Mastery | 5 | 23 | 4 | 3 | 3 | 3 | 3 | 1 | 1 | 1 | 1 |
| 19 | +6 | Epic Boon | 5 | 24 | 4 | 3 | 3 | 3 | 3 | 2 | 1 | 1 | 1 |
| 20 | +6 | Signature Spells | 5 | 25 | 4 | 3 | 3 | 3 | 3 | 2 | 2 | 1 | 1 |