<!-- Copyright (c) 2026 Jeremy Wright. All rights reserved. Published for review only; no licence granted. See LICENSE.txt -->

# Role templates

**42 roles. Generation scaffolding, not characters.**

A role biases what the AI invents so the fifteenth villager doesn't sound like
the first, and says where to get a stat block if one is ever needed. Spec:
[`../../../docs/npc-containers.md`](../../../docs/npc-containers.md) §5.

**Each file is 20–30 lines and stays that way.** A role that grows past that is
being written as a character, which is the mistake this directory exists to
prevent.

---

## The split

| | |
|---|---|
| [`town/`](town/) — **20** | people who live inside a settlement |
| [`world/`](world/) — **12** | people who live outside one |
| [`hostile/`](hostile/) — **10** | people who **command** other people at you |

They're separated because they're different generation contexts. A town role
knows *who*; a world role knows *where*. Ask for a villager and you should get
someone with neighbours; ask for someone on the road and you should get someone
who watches empty country.

### town/

tavern-owner · merchant · fence · artisan · entertainer · vagabond · child ·
priest · hedge-caster · healer · scholar · official · noble · guard · soldier ·
thug · servant · moneylender · sailor · carter

### world/

farmer · miner · hunter · forester · shepherd · fisher · ferryman · hermit ·
pilgrim · bandit · tinker · scout

### hostile/ — the command tier

bandit-captain · raider-chief · crime-boss · mercenary-captain · cult-leader ·
zealot · renegade-mage · beast-handler · corrupt-magistrate · spymaster

**The other 32 already escalate into hostility** — every one carries an
`Escalation` section. What none of them do is **give orders**, and that was the
gap. These come with a `commands:` field so dropping one in produces an
**encounter**, not a person.

They also carry an extra section the others don't: **`## Way out that isn't a
fight`.** Every single one of these can be resolved without initiative, and most
of them would prefer it. A mercenary captain wants the contract bought out; a
bandit captain wants a toll; a beast-handler folds the moment you take the
animals. **If every hostile encounter becomes a fight, the tier isn't being used
properly.**

---

## The shape

```yaml
---
role:              # slug, matches filename
stat_block:        # SRD reference — consulted ONLY if plausible_combat
plausible_combat:  # true | false | sometimes | rarely | never
domain:            # town | world
---

## Knows      what this kind of person has access to that others don't
## Wants      3-4 concrete, small, immediate
## Found      where they physically are
## Voice      how they talk — the part that stops every NPC sounding alike
## Hooks      2-3 ways this role becomes a plot
## Escalation what happens when the plot needs them to matter
```

**`Escalation` is not "give them a bigger stat block."** For most roles it's the
opposite — what escalates is *what they know*, *what they witnessed*, or *who
sent them*. The tanner never becomes a boss fight; the tanner recognises the
maker's mark.

**`plausible_combat: false` means no stat block is retrieved and none is written
into the container.** Most people in a world never roll initiative, and giving
the shepherd a stat block is how you end up with a DM who thinks the shepherd is
an encounter.

`child` is `never`. That one isn't a tuning value.

---

## Using them

1. The plot needs a person → pick the role that fits
2. Generate from `Voice` + `Wants` + the trait/name tables in `../`
3. Write the container — `canon/locations/<place>/npcs/<slug>.md`
4. The role is **not** copied into the container. It's scaffolding, and it's
   done once the person exists.

`role:` is recorded in the container as a pointer, so a later session can see
what shape the person was built from without re-reading this directory.

---

## Adding a role

Only when a real NPC didn't fit any of the 32 — and then write it **after the
fact**, from the person who needed it. Roles invented in advance are guesses;
roles extracted from a character who already worked are evidence.

**Not a role: "elder."** Age is a modifier on farmer, official or priest. Add
roles for adjectives and 32 becomes 80, none of them load-bearing.
