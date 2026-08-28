<!-- Copyright (c) 2026 Jeremy Wright. All rights reserved. See LICENSE.txt -->

> This work includes material from the System Reference Document 5.2 ("SRD 5.2")
> by Wizards of the Coast LLC, available at https://www.dndbeyond.com/srd. The
> SRD 5.2 is licensed under the Creative Commons Attribution 4.0 International
> License, available at
> https://creativecommons.org/licenses/by/4.0/legalcode.

# Articles — the SRD, one file per thing

**Built 2026-08-27.** The reference corpus as addressable files instead of a
2 MB dump.

| type | count | |
|---|---|---|
| [`spells/`](spells/) | **301** | every SRD spell |
| [`magic-items/`](magic-items/) | **229** | every SRD magic item |
| [`rules/`](rules/) | **41** | ⚠️ **only the TAGGED glossary entries** — conditions · actions · areas of effect · hazards · attitudes |
| [`feats/`](feats/) | **17** | origin · general · fighting style · epic boon |
| [`classes/`](classes/) | **12** | **232 features**, one file per class |
| [`subclasses/`](subclasses/) | **12** | one per class, which is all the SRD ships |
| [`backgrounds/`](backgrounds/) | **4** | Acolyte · Criminal · Sage · Soldier |
| **total** | **616** | plus `index.json` |

---

# ⭐ Why "article", and why not "element"

**`element` was taken.** A module's `elements/` are the authored pieces of an
adventure — a wand, an ending, a set of guards — and they carry `constraints`
that bind the DM. ⛔ **Reusing the word would have made two unrelated things
share a name in a system where `elements/` already has rules attached to it.**

**`entry` and `record` were also taken** — 80 and 102 uses, and both are
load-bearing: a *ledger entry* is the atom of `ledger.jsonl`.

> ### An article is a single reference thing that can be loaded on its own.
> **One spell. One item. One condition.**

⭐ **The point of the split is that a DM loads what it needs.** `Fireball` is
1.5 KB. The dump it came out of is 1.4 MB. **A DM that has to grep 363 pages to
recall a spell is paying for the whole book on every question.**

---

# The shape every article shares

```yaml
---
article: <type>        # spell | magic-item | rule | feat
name: "<display name>" # verbatim from the source
slug: <kebab-case>     # the filename, without .md
...type-specific fields...
source: "SRD 5.2"
---

# <name>

*<one-line summary line — the thing printed under the name in the book>*

<the text>
```

**Plus the CC-BY attribution comment at the top of every file**, which is
[`../README.md`](../README.md)'s standing rule for this directory and a licence
condition rather than a style choice.

## Conventions

| | |
|---|---|
| **slug** | lowercase, non-alphanumerics collapsed to `-`. ⭐ **Verified unique within each type** — a collision would silently overwrite |
| **body** | reflowed from the PDF's hard line breaks; hyphenated line-splits rejoined |
| **`source`** | present on every article so a future non-SRD import is distinguishable |
| **verbatim** | ⛔ **names and rules text are never paraphrased.** Everything here is reproducible under CC-BY only because it is unaltered |

---

# The seven schemas

## `spell`

```yaml
article: spell
name: "Fireball"
slug: fireball
level: 3                    # 0 for a cantrip
school: Evocation
classes: [Sorcerer, Wizard] # may be empty
casting_time: "Action"
range: "150 feet"
components: "V, S, M (a ball of bat guano and sulfur)"
duration: "Instantaneous"
concentration: false        # derived: duration starts "Concentration"
ritual: false               # derived: casting_time contains "Ritual"
summons_stat_block: false   # true for the 4 that summon a creature
source: "SRD 5.2"
```

⭐ **`concentration` and `ritual` are derived, not transcribed.** They live
inside prose in the source, and every consumer needs them as booleans —
`state-formats.md`'s `conc` events, and any "what can I still hold?" question.

## `magic-item`

```yaml
article: magic-item
name: "Amulet of Proof against Detection and Location"
slug: amulet-of-proof-against-detection-and-location
category: Wondrous Item     # Armor|Potion|Ring|Rod|Scroll|Staff|Wand|Weapon|Wondrous Item
subtype: "Any Ammunition"   # the parenthetical after the category, often ""
rarity: "Uncommon"          # ...|Legendary|Artifact|Rarity Varies
attunement: true
attunement_note: "by a Druid"   # the qualifier, often ""
source: "SRD 5.2"
```

⭐ **`attunement` is split into a boolean and a qualifier** because they answer
different questions. **The boolean is what a filter needs; the qualifier is what
a DM needs**, and one field would have served neither.

⚠️ **`rarity` is not a clean ordinal** — `Rarity Varies` exists and is not a
degree. **Do not sort on it.**

## `rule`

```yaml
article: rule
name: Paralyzed
slug: paralyzed
tag: Condition              # Condition|Action|Area of Effect|Hazard|Attitude
source: "SRD 5.2"
```

**Only the glossary entries the SRD itself tags** are here. ⭐ **The tag is the
source's, not ours** — the book prints `Blinded [Condition]`, and inventing a
taxonomy on top of that would have been our judgement wearing the SRD's
authority.

## `feat`

```yaml
article: feat
name: Archery
slug: archery
category: Fighting Style    # Origin|General|Fighting Style|Epic Boon
prerequisite: "Fighting Style Feature"   # often ""
source: "SRD 5.2"
```

## `class` and `subclass`

```yaml
article: class          # or: subclass
name: Wizard
slug: wizard
class: Wizard           # subclass only — which class it belongs to
features: 10            # count, for cross-checking against core.md
source: "SRD 5.2"
```

**Features are `## Level N: Name` sections in the body.** ⭐ **One file per
CLASS, not per feature** — a class's features are read together *("build a
level 5 wizard")* far more often than singly, and a class file stays under
400 lines. **Lookup by feature name is a grep, and `core.md` already indexes
them by level.**

## `background`

```yaml
article: background
name: Acolyte
slug: acolyte
abilities: "Intelligence, Wisdom, Charisma"
feat: "Magic Initiate (Cleric) (see “Feats”)"
skills: "Insight and Religion"
tool: "Calligrapher’s Supplies"
source: "SRD 5.2"
```

---

# ⛔ What is NOT here, and why

| | |
|---|---|
| **Monsters** | already extracted as [`../monsters.md`](../monsters.md), 112 pages. ⚠️ **Not re-split** — it works, and splitting it is churn, not value |
| **Species** | already [`../species.md`](../species.md) |
| **Class progression** | [`../../2024/core.md`](../../2024/core.md) — a table, not an article set. ⭐ **`classes/` holds what the features DO; `core.md` holds when you get them** |
| **Equipment** | [`../../2024/equipment.md`](../../2024/equipment.md) — weapons, armour, gear, mounts. **Tables: a weapon is a row, not an article** |
| ⛔ **~130 UNTAGGED glossary terms** | *Blindsight, Bloodied, Bonus Action, Cover, Reach…* **Attempted and backed out — SRN-46.** A shape heuristic pulled in table fragments wearing the same shape *(`AC Substance AC Substance`, `S Somatic`, `Size Water`)*, and **any filter would have been tuned by eye against 128 entries** — the exact failure this file is written against. **41 clean beats 169 contaminated.** The real fix is reading the PDF's font weights, not its text |
| **Ammunition, tools, services, components** | priced in tables with different shapes — see `equipment.md` |

## ✅ Stat blocks — cut, then reattached to the right spells

**`pdftotext` reading order files stat blocks unreliably across page
boundaries.** Fireball had absorbed *Find Steed*'s **Otherworldly Steed** —
1,300 characters of another spell's creature under the wrong name — and
Antipathy/Sympathy had *Animate Objects*' **Animated Object**.

**All four were cut first, then placed by line range under their real owners:**

| block | belongs to | |
|---|---|---|
| Otherworldly Steed | `find-steed` | ⭐ was under **Fireball** |
| Animated Object | `animate-objects` | ⭐ was under **Antipathy/Sympathy** |
| Giant Insect | `giant-insect` | its own |
| Draconic Spirit | `summon-dragon` | its own |

**`summons_stat_block: true` marks the four that have one.** ⭐ **Cut first,
attribute second** — the intermediate state lost real content from two summon
spells, and that was the correct trade while ownership was unknown.

---

# ⭐ What extraction taught, three times in one session

> ## An enum that does not cover a source variation produces output that looks complete, because what is missing leaves no hole.

| | dropped | found by |
|---|---|---|
| **`-layout` column interleave** | table cells | a proficiency-bonus formula check |
| **`Rarity Varies` missing from the rarity enum** | **7 magic items, including Spell Scroll** | asking why `Scroll` was zero |
| **wrapped prerequisite parenthetical** | **6 feats** | `Fighting Style` being zero |

> ### A count is only evidence if you know what it should be.
>
> **`Fighting Style: 0` was checkable. `General: 1` was not, and would have
> shipped.** ⭐ **The zero saved the one beside it.**

## ⭐ The best check available: two extractions of the same fact

**`core.md`'s progression tables and `classes/`'s feature sections come from
DIFFERENT PAGES of the SRD** — the table on the class's opening spread, the
descriptions across the pages after it. **So the feature names are extracted
twice, independently.**

> ### Ten of twelve classes match EXACTLY.

**The two that differ, differ for a known reason and neither is wrong:**

| | |
|---|---|
| **Fighter** | the table lists *Action Surge (one use)* at 2 and *(two uses)* at 17; the article describes **Action Surge** once. Same for **Indomitable** *(one/two/three uses)* |
| **Warlock** | *Mystic Arcanum (level 6 spell)* … *(level 9)* are four table rows and **one** feature |

⭐ **The table tracks a feature that UPGRADES; the article describes it once.**
Different granularity, not a contradiction — and the fact that only these two
classes differ is itself the evidence that both extractions are sound.

**When SRN-45's remaining work lands, re-run this comparison.** ⛔ **A new
mismatch means one of the two is wrong, and it names the class to look at.**

---

**So every extraction here is checked against something other than itself:** a
formula, a cross-class invariant, a category that must not be empty, or a marker
that cannot legally appear in the output. ⛔ **Eyeballing 588 articles is not a
verification method, and re-reading your own parser's output is not either.**

⚠️ **What is NOT verified:** article **names and prose are transcribed, not
proofread against the source.** A misspelling is possible. **A missing required
field, a duplicate slug, or a body containing another article's content is
not** — all three are checked mechanically.
