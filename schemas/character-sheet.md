<!-- Copyright (c) 2026 Jeremy Wright. All rights reserved. Published for review only; no licence granted. See LICENSE.txt -->

# Character file format

One `.md` per character. **YAML frontmatter is the machine-readable sheet; the
body is for the model.** Code parses the frontmatter, the model reads the whole
file.

See [`seren.md`](seren.md) for a worked example — check the format against that
before bulk-importing.

---

## Two rules that matter

### 1. This is the SHEET, not the STATE

The file records what the character **is** (`Cosmic Omen: 4 uses per long rest`),
never what they **currently have** (`2 uses left`). Current HP, expended slots,
conditions and concentration are runtime state and live nowhere in this
directory. See [`../docs/architecture.md`](../docs/architecture.md) §2.

The only HP that belongs here is `max`.

### 2. Mark what you don't know

Anything not definitively present in the source gets `TODO:` and stays wrong-free
rather than being guessed. **The DM will act on these numbers.** An invented
skill modifier becomes a wrong roll in play, silently, forever.

Where a value is *derived* rather than copied, say so in a comment — the
derivation is auditable, an assertion isn't.

---

## Frontmatter schema

```yaml
name:                 # display name
pronouns:             # used by the DM in narration
species:              # 2024 term (was "race")
class:
subclass:
level:
campaign:             # or null for unassigned
ruleset:              # "2024" or "2014" — they differ enough to matter
proficiency_bonus:

abilities:            # raw scores, not modifiers
  str: dex: con: int: wis: cha:

saves_proficient:     # list of ability keys
skills_proficient:    # list
skills_expertise:     # list, if any
skill_modifiers:      # {skill: modifier} — use INSTEAD of the two lists above
                      # whenever item bonuses make proficiency underivable.
                      # The DM needs the modifier; the classification is a
                      # convenience. Never guess a classification to fill a field.

ac:
speed:                # {walk:, fly:, swim:, climb:}
hp:
  max:                # ONLY max. Current HP is runtime state.
  hit_dice:

senses:
  darkvision:
  passive_perception:
  passive_investigation:
  passive_insight:

resistances:          # damage types
immunities:
languages:
proficiencies:
  armor: weapons: tools:

spell_slots:          # {1: 4, 2: 3, ...} — by level, max
spellcasting_ability:
spell_save_dc:
spell_attack_bonus:

resources:            # every limited-use feature, explicitly
  - name:
    uses:
    recharge:         # short_rest | long_rest | turn | dawn | special

conditions_of_note:   # anything permanently on the character
```

---

## Body sections

Use these headings, in this order. Omit any that don't apply.

```markdown
## Actions
## Bonus Actions
## Reactions
## Other / No-Action
## Features & Traits
## Spells
### Cantrips
### Prepared / Known
### Rituals
## Equipment
## Roleplay
```

**`## Roleplay` is not optional and not decoration.** It's what stops the DM
narrating a generic adventurer. Voice, temperament, what they want, what they
fear, who they owe, how they enter a room. If the source dump has nothing, write
`TODO:` and flag it — a mechanically perfect character the DM can't *voice* is
only half imported.

---

## Notes on importing from D&D Beyond

The web sheet dumps labels without values in several places. Known gaps to watch:

- **Skill modifiers** usually don't come through — only the skill names. Derive
  proficiency from passive scores where possible (`passive = 10 + mod + prof`),
  mark the rest `TODO`.
- **Saving throw values** likewise. Class defaults are usually safe but say so.
- **Spell slots** aren't shown; derive from class + level and note it.
- **Limited-use counters** show current/max (`4/4`) — take the max, discard the
  current, it's state.
- **Subclass** often isn't named outright; infer it from the feature list and
  record the inference.
