<!-- Copyright (c) 2026 Jeremy Wright. All rights reserved. Published for review only; no licence granted. See LICENSE.txt -->

# NPC containers

**Spec'd 2026-08-24.** How people persist in Seren.

> ## The one rule
>
> **A container is an empty vessel the AI fills at the moment an NPC is created,
> and then holds state in.** Nothing is pre-populated. No town is generated in
> advance. The world accumulates people as the player meets them.

This is the *persistence* half of the design decision in
[`../npcs/README.md`](../npcs/README.md): generation was never the problem. The
AI can invent a tavern keeper on demand. **What it cannot do is invent the same
tavern keeper in session 9 that it improvised in session 3.** Containers are the
fix.

---

## 1. Structure

**Storage is by location, INSIDE the campaign. NPCs are saved to the town where
they were met.**

> ⚠️ **Corrected 2026-08-24.** This section originally placed containers under a
> **top-level** `canon/`. That was wrong: **canon is campaign-bound** — what is
> true in one campaign is not true in another. The top-level
> [`../canon/`](../canon/) holds **portable** canon instead (a character's
> `bible.md` and `secrets.md`, imported setting reference) — template layer. The
> campaign's own `canon/` holds what play established — instance layer. Same
> split as sheet-vs-state, one level up. See
> [`campaign-start.md`](campaign-start.md) §1.

```
LIVE/<campaign>/canon/locations/riverbend/
    state.md                        what's true about this place
    charactermap.md                 index — who is here, links only
    npcs/
      hal-tanner.md                 the container
      hal-tanner-interactions.md    accretes, one entry per contact

npcs/
    tables/
      roles/
        town/                       20 roles — people who live in a settlement
        world/                      12 roles — people who live outside one
      names/ traits/ hooks/         seeds (mjmcphee — see §6)
    adventurers/                    pre-built rival adventurers (built)
```

**Nobody's file ever moves.** An NPC met in Riverbend lives in Riverbend
permanently. If they turn up in Kelvin's Ford, *that* location's
`charactermap.md` links across to the Riverbend file. Presence is an index;
residence is storage.

**There is no `named/` directory.** Promotion is a `status:` field, so a
character becoming important never changes a path or breaks a link.

---

## 2. The container

`LIVE/<campaign>/canon/locations/<place>/npcs/<slug>.md`

Written **once**, at the moment the NPC is created. Amended only when what they
*are* changes — not when something happens to them. That goes in the
interactions log.

```yaml
---
name:
slug:
role:              # the role template used — see §5
location:          # where they were met, and where this file lives
status:            # met | named
first_seen:        # session ref — provenance, non-negotiable
stat_block:        # SRD/Open5e reference. ONLY if combat is plausible.
                   # Omit for the tanner. Include for the bandit.
want:              # ONE line. What they are pushing for.
voice:             # 1-2 lines. How they actually talk.
tell:              # a physical habit to hang narration on
---

## Knows

- fact: …
  visibility: true | known | suspected | false
```

**`Knows` carries visibility or the DM leaks the plot.** Architecture §3. An NPC
without visibility tags cannot hold a secret, because the model receives the
whole file and has no way to tell what it's allowed to say.

**`false` is the tag people delete. Don't.** A person who believes something
untrue is good drama, and if it isn't written down as untrue the DM will
"helpfully" correct it in narration and nobody will notice the scene died.

### Why `secrets.md` isn't here

**`secrets.md` is for the party.** PCs get one because a hidden subplot about a
player character needs room — a curse they don't know about, a lie in their
backstory, who is actually hunting them.

An NPC's hidden material fits in `Knows` with `visibility: true`. **A separate
`secrets.md` is created for an NPC only when one earns it** — a recurring
antagonist with real hidden structure. Not the tanner.

### ⚠️ `secrets.md` is a LIVING file, not an authored one

**Clarified 2026-08-25 (Jay).** Every other reference to `secrets.md` in these
docs implies it gets written once, at campaign start, and then read. **That is
wrong, and it wastes the most useful surface the DM has.**

> **It is the DM's private notebook for one person.** Hidden facts are the seed.
> Everything the DM later wants to *maybe* surface gets filed here as it occurs
> to them, mid-campaign, and sits until a trigger matches.

That gives it two halves, and they behave differently:

| | what it holds | how it changes |
|---|---|---|
| **facts** | what is true and hidden, visibility-tagged | **append only.** Never rewrite something already true. |
| **threads** | what *could* become true — not true yet | **the DM adds these during play.** Spent ones are marked, not deleted. |

**Threads use the `ideas.md` entry format** *(trigger · hook · cost · status)*
from [`../campaigns/README.md`](../campaigns/README.md), because they are the
same thing scoped to one person. An untriggered thread is free; a spent one
commits.

**This is what distinguishes it from the interactions log**, and the three-way
split is worth holding:

| file | holds | tense |
|---|---|---|
| `<slug>-interactions.md` | what happened | **past.** Factual, append-only. |
| `<slug>-secrets.md` | what is hidden, and what might happen | **present and conditional.** |
| `ideas.md` | what might happen, attached to nobody yet | **conditional.** Campaign-wide. |

**So a named NPC the party keeps returning to accretes a secrets file whether or
not they started with one** — the moment the DM has a thought worth keeping about
them, that is where it goes. That is the promotion path from furniture to
character, and it now has a mechanism.

---

## 3. The interactions log

`LIVE/<campaign>/canon/locations/<place>/npcs/<slug>-interactions.md`

Created **lazily**, on the first exchange worth recording. Appended thereafter.
Never rewritten.

```markdown
## S07 — 2026-09-14
Player asked about the missing shipment. Hal deflected, then admitted he'd sold
the manifest to someone he wouldn't name. Player let it go. **He noticed that.**
→ promoted: player used his name unprompted.
```

**This is the sheet-vs-state split from architecture §2, applied to people.** The
container says who Hal *is* and stays stable. The log says what *happened* and
only grows. Keeping them apart is what stops the container from being rewritten
every session until it's unrecognisable.

**One entry per session per NPC**, not per exchange. If nothing happened worth a
line, write nothing.

---

## 4. `charactermap.md` — the load-bearing file

```markdown
# Riverbend — who is here

## Residents
- Hal Tanner — tanner, sells to the garrison → `npcs/hal-tanner.md`
- Mother Ceric — priest at the waystone → `npcs/mother-ceric.md`

## Currently present
- Vess Greyleaf — passing through, hired as a guide → `../../../npcs/adventurers/vess-greyleaf.md`
```

**Links and one line of role. Nothing else, ever.**

This is what keeps a long campaign inside a context window: the DM reads the map,
then loads only the containers for people actually in the scene. The moment
someone starts writing personality into `charactermap.md`, that property is gone
and the file becomes another thing to maintain.

---

## 5. Role templates — the "NPC classes"

`npcs/tables/roles/<role>.md`

**A role is generation scaffolding, not a character.** It biases what the AI
invents so that the fifteenth villager doesn't sound like the first, and it says
where to get a stat block if one is needed.

**They are LEAN — 20 to 30 lines.** A role that grows past that is being written
as a character, which is the mistake this whole directory exists to avoid.

```yaml
---
role: tavern-owner
stat_block: Commoner        # only consulted if plausible_combat is true
plausible_combat: false
---

## Knows
Local gossip · who drinks with whom · who is behind on a tab · who came
through and when · which rooms are let and to whom

## Wants
- a debt paid
- a nuisance gone — the garrison, a regular, a smell
- their kid to come home
- one quiet night

## Found
Taproom · cellar · the yard out back · market at dawn

## Voice
Talks while doing something else and rarely stops moving. Answers the question
before the one you asked. Uses your name more than necessary.

## Hooks
- an overheard conversation they'd rather you hadn't
- a room let to the wrong person
- a tab someone else settled

## Escalation
If the plot needs them dangerous: **they were something else before this.**
Stat block becomes **Warrior Veteran**, and the apron is recent.
```

### The set — 32, built 2026-08-24

**Written and in place:** [`../npcs/tables/roles/`](../npcs/tables/roles/) —
**20 town** + **12 world**, 28–29 lines each.

Split because they're different generation contexts. A town role knows *who*; a
world role knows *where*. The world set — farmer, miner, hunter, forester,
shepherd, fisher, ferryman, hermit, pilgrim, bandit, tinker, scout — exists so
that "someone on the road" produces a person who watches empty country for a
living, not a villager standing in a field.

**These are ours to write.** SRD has stat blocks, not social roles — there is no
"tavern owner" in any rules corpus, and there shouldn't be.

| role | stat block | combat plausible |
|---|---|---|
| **tavern-owner** | Commoner | no |
| **merchant** | Commoner | no |
| **fence** *(smuggler, receiver)* | Bandit / Spy | sometimes |
| **artisan** *(smith, tanner, cooper)* | Commoner | no |
| **farmer** | Commoner | no |
| **sailor** *(dockhand, ferryman)* | Commoner / Bandit | sometimes |
| **entertainer** *(minstrel, player)* | Commoner | no |
| **vagabond** *(beggar, drifter)* | Commoner | no |
| **child** | Commoner | **never** |
| **priest** | Priest / Priest Acolyte | rarely |
| **hedge-caster** *(cunning woman, local mystic)* | Mage / Priest Acolyte | sometimes |
| **healer** *(herbalist, midwife)* | Priest Acolyte / Commoner | no |
| **scholar** *(scribe, archivist)* | Commoner / Mage | no |
| **official** *(clerk, reeve, factor)* | Noble / Commoner | no |
| **noble** | Noble | rarely |
| **guard** *(watch)* | Guard | **yes** |
| **soldier** *(off-duty, mercenary)* | Warrior Veteran | **yes** |
| **thug** *(enforcer, tough)* | **Tough** | **yes** |
| **scout** *(tracker, outrider)* | Scout | **yes** |
| **hunter** *(trapper, fowler)* | Scout / Commoner | sometimes |


> ⚠️ **Stat block names verified against SRD 5.2, 2026-08-26.** **Four** of the
> names this file used are **5.1 names**. Corrected from the source, not from
> memory: **Acolyte → `Priest Acolyte`** *(AC 13, HP 11)*, **Veteran →
> `Warrior Veteran`** *(AC 17, HP 65)*, **Thug → `Tough`** *(AC 12, HP 32)*.
>
> ⭐ **The Thug was renamed, not cut** *(corrected 2026-08-26)*. An earlier pass
> grepped the full dump for "Thug", found zero occurrences, and concluded it had
> been removed from 5.2. It is **`Tough`** — same HP 32, same CR 1/2, same Pack
> Tactics, same mace. The new name was sitting in this container's own
> parenthetical the whole time: *thug (enforcer, **tough**)*. **A rename is not
> an absence, and zero hits on the old name does not establish one.**
>
> ⭐ **`Tough Boss`** *(AC 16, HP 82, CR 4, Pack Tactics, Warhammer 2d8+3)* is
> the command-tier block this file records as missing below — someone who gives
> orders to the toughs.

**Twenty covers a world.** Add one only when a real NPC doesn't fit any of
them — and then write it *after the fact*, from the person who needed it.

**Deliberately not a role: "elder."** Age is a modifier on farmer, official or
priest, not a job. The moment you add roles for adjectives, twenty becomes
eighty and none of them are load-bearing.

### `plausible_combat` earns its own field

If it's `false`, **no stat block is retrieved and none is written into the
container.** Most people in a town will never roll initiative, and giving the
tanner a stat block is how you end up with a DM who thinks the tanner is an
encounter.

---

## 6. What we take from outside

**Open5e / dnd5eapi supply `stat_block:` and nothing else.** Their monster
endpoints carry SRD humanoids — Commoner, Guard, Priest, Noble, Spy,
Bandit, Warrior Veteran, Priest Acolyte, Scout. Those are *mechanics with a job title*: no
name, no want, no voice. They fill exactly one field.

That is the correct amount of Open5e, and it matches the existing rule: pre-build
only what must be mechanically correct.

> ⚠️ **The stat blocks above are confirmed for SRD 5.1 (2014).** Verify names and
> content against SRD 5.2 / 2024 before wiring retrieval — the same trap
> [`open-source-resources.md`](open-source-resources.md) flags, and the one the
> character roster already demonstrated.

**[mjmcphee/dnd-npc-generator](https://github.com/mjmcphee/dnd-npc-generator)**
*(Mike McPhee, MIT, 2024-native)* is the only seed source found → `npcs/tables/`.

⚠️ **It is small** — 1 star, 4 commits, tables hardcoded as inline Python dicts
rather than data files. **Useful as a starting point; not a corpus.**

The need it addresses is real regardless: **variety at the point of
generation.** Without seed tables, improvised NPCs drift toward a single voice
and the world ends up sounding like one person doing accents. If mjmcphee's
lists are too thin, generate our own — the requirement is breadth, not
provenance.

**Adventures are not a container source.** 1Shot and the rest do contain real
NPCs, but they arrive welded to a plot and their licensing varies per adventure.
Good for inspiration, bad for import.

---

## 7. Lifecycle

```
   player interacts
        -> AI generates the person from a role template + trait tables
        -> queued for capture
   session close
        -> container written        LIVE/<campaign>/canon/locations/<place>/npcs/<slug>.md
        -> charactermap.md updated
        -> interactions log created or appended
```

**Written at session close, never mid-turn.** Architecture §5 and SelfActual
vault principle #7. Pod data reflects finalised state — and practically, it
means one small batch of writes instead of fighting the filesystem during play.

**Promotion:** `status: met` → `status: named` the first time the player
remembers the NPC's name unasked. That's the moment they stop being furniture.
It changes a field and nothing else — no move, no broken links.

---

## 8. The hostile stack — spec'd 2026-08-24, not built

**Baddies come in three weights**, and collapsing them is how you get either a
nemesis who resets every session or a random encounter with a tragic backstory
nobody asked for.

| tier | what it is | lives in | persistence |
|---|---|---|---|
| **hostile** ✅ | generated on the spot when the plot needs a threat | [`../npcs/tables/roles/hostile/`](../npcs/tables/roles/hostile/) — **10 built** | none — unless they survive and start recurring, at which point promote them |
| **antagonist** | the recurring nemesis | `npcs/antagonists/` | **interactions log is mandatory** |
| **front** | a faction with an agenda and a clock | `campaigns/fronts/` | advances whether the party engages or not |

*(Jay's word for the middle tier is "baddies." The directory is named for the
model, not the operator.)*

### hostile/ — ✅ BUILT 2026-08-24, 10 files

**Most of this already exists.** Every one of the 32 roles carries an
`Escalation` section that turns them hostile — the tavern-owner who was
something else before this, the fence who will trade the party for the party.

✅ **The command tier is built** *(corrected 2026-08-26 — this paragraph said it
was missing, and it had already been written).* Ten roles in
[`../npcs/tables/roles/hostile/`](../npcs/tables/roles/hostile/) — **people who
command other people at you**, which is what separates them from `town/` and
`world/`.

> bandit-captain · cult-leader · crime-boss · mercenary-captain · zealot ·
> renegade-mage · beast-handler · corrupt-magistrate · **raider-chief** ·
> **spymaster**

⭐ **Stat block for the tier: `Tough Boss`** *(SRD 5.2 — AC 16, HP 82, CR 4,
Pack Tactics, Warhammer 2d8+3)*. Point `crime-boss` and `mercenary-captain` at
it rather than inventing one — **SRN-33**.

Same 20–30 line format as any role, plus one field:

```yaml
commands:    what they bring with them — "4-6 Bandits, one Scout on the ridge"
```

That's what makes dropping one in produce an **encounter** rather than a person.

### antagonists/ — ✅ BUILT 2026-08-24, six files

**Six, maybe eight. Never twenty.** See
[`../npcs/antagonists/README.md`](../npcs/antagonists/README.md).

```
npcs/antagonists/                                    TEMPLATE layer
  <slug>.md                 who they are + the grudge prompt
  <slug>-secrets.md         if earned  (3 of 6 earned one)

LIVE/<campaign>/canon/antagonists/                  INSTANCE layer
  <slug>-interactions.md    MANDATORY — this is how they learn
```

> ⚠️ **Corrected 2026-08-24, same error class as §1.** This block originally put
> the interactions log next to the template at top level. It cannot live there:
> the log is **what happened in play**, and play is campaign-bound. So the
> template stays portable and the log is created at campaign instantiation.
>
> **"Mandatory" means mandatory at campaign instantiation, not at template
> creation.** A template with no log is correct; a *live* antagonist with no log
> is the failure this tier exists to prevent.
>
> **A sibling of `canon/locations/`, not inside it** — a captured NPC is stored
> in the town where they were met, but antagonists **travel**, and binding one
> to a location would be a lie the first time they follow the party.

**Two fields were added during the build** and are not in the list below:
`attaches_to:` and `fallback:`. A party is 3-4 of 14 characters, and four of the
six hang off a specific PC's hook — without a declared dependency the DM finds
out at campaign creation that two of their nemeses are unusable. The fallback
keeps them usable anyway.

Three fields only this tier needs:

```yaml
grudge:      why they keep coming back — ONE line, and it is PARTY-RELATIVE
exit:        resolved | turned | killed — decided NOW, not later
escalation:  what changes on appearance 2, 3, 4+
```

**Three rules, all of them the difference between a nemesis and furniture:**

1. **They accumulate and never reset.** By the fourth meeting they know the
   party fights at range and they are still angry about the horse. The
   interactions log is the mechanism, which is why it isn't optional here.
2. **They need an exit, decided up front.** A nemesis who can never be resolved
   becomes a recurring tax. *Turned* is the best of the three, and killing one
   should cost the party something.
3. **Not core to the campaign.** If their death would end the plot, they are a
   **front**, not an antagonist. This is a constraint on how they're written,
   not a footnote.

**Keep the bench small.** The entire value is *"oh, it's him again"* — which
requires the player to hold all of them in their head at once. Twenty pre-built
nemeses is twenty strangers.

### fronts/ — see [architecture.md](architecture.md) §6

Not specified here. A front holds what is **true** and what is **in motion**,
never what happens next. That's the piece that makes the world move on its own,
and the antagonists hang off it.

---

## 9. Open

- **The capture threshold.** *"Interacted"* is doing a lot of work. Speaking to
  someone shouldn't be enough or you accumulate doormen. Proposed: **the player
  asks them something, or the DM gives them a name.** Not yet settled.
- **Hidden material is honour-system, full stop** — the player owns the
  filesystem, and it works the way not peeking behind a DM screen works: by
  agreement.
  > ⚠️ **Corrected 2026-08-26.** This bullet previously claimed sub-pod ACLs
  > make it a real partition, and called it *"the first feature that genuinely
  > requires the pod."* **That is wrong** — the player is the operator, and
  > **ACLs do not partition someone from their own vault.** It only becomes a
  > real boundary with a second person, which is a different product.
  > Architecture §5b carries the full correction; what the pod *would* buy is in
  > [`pieces-selfactual.md`](pieces-selfactual.md).
- **Nothing enforces the visibility tags yet.** They're a writing convention
  until code reads them and splits the context by tag.
