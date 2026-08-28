<!-- Copyright (c) 2026 Jeremy Wright. All rights reserved. Published for review only; no licence granted. See LICENSE.txt -->

# Antagonists — six recurring nemeses

**Built 2026-08-24.** The middle weight of the hostile stack
([`../../docs/npc-containers.md`](../../docs/npc-containers.md) §8): heavier than
a dropped threat, lighter than a front.

> ## The one thing this directory is for
>
> ### *"Oh. It's him again."*
>
> That reaction requires the player to hold **all of them at once**. Six is not
> a starting number — it is the ceiling. Twenty pre-built nemeses is twenty
> strangers.

---

## The six

| # | axis — what they want | who | chassis | exit | attaches to |
|---|---|---|---|---|---|
| 1 | something **from** the party | [Maelis Corr](maelis-corr.md) | Wizard 3 *(Abjurer)* | resolved | Zephyr / Llewellyn |
| 2 | the party **stopped** | [Ilma Danneke](ilma-danneke.md) | Bard 3 *(Lore)* | turned | **party-wide** |
| 3 | the party **destroyed** | [Corwen Hale](corwen-hale.md) | Fighter 3 *(Battle Master)* | **killed** | Jornis |
| 4 | the party **recruited** | [Ossa Rell](ossa-rell.md) | Wereboar *(SRD, CR 4)* | turned | Zephyr |
| 5 | **does not know** they are one — and is **wrong** | [Teodor Wick](teodor-wick.md) | Scout *(SRD)* — not a class build | resolved | **party-wide** |
| 6 | **is right** | [Iselde Varr](iselde-varr.md) | Rogue 3 *(Thief)* | turned | Deerx |

**Secrets files, where earned:** Maelis, Ossa, Iselde. The other three carry
their hidden material in `Knows` with `visibility: true`, per the container
spec — a separate file is earned, not automatic.

### Why the axis, and not "social / martial / arcane"

Class variety changes **what dice get rolled**. For someone the player meets five
times, what has to vary is **what scenes they generate**. Six vendettas would be
one nemesis with six faces — and that is the failure mode a small bench is most
exposed to.

**5 and 6 are a deliberate pair.** Teodor is sincerely wrong; Iselde is entirely
right. Running both is the whole spread, and neither works nearly as well alone.

---

## The three rules

### 1. They accumulate and never reset

By the fourth meeting they know the party fights at range and they are **still
angry about the horse.**

**The interactions log is the mechanism, which is why it is not optional at this
tier.** Every file names its own log and says what specifically to record in it,
because what accumulates differs per antagonist: Corwen accumulates *tactics*,
Ilma accumulates *what she was told*, Ossa accumulates *refusals*, Iselde
accumulates *the shape of the party's attempts*.

### 2. They need an exit, decided up front

`exit:` is the **designed** resolution — a commitment by the author about what
closure looks like. **It is not a constraint on play.** Anyone here can eat a
crit.

Its job is to stop a nemesis becoming a recurring tax. **Turned is the best of
the three** (three of six), and **killing one should cost the party
something** — which is why exactly one is written with no good ending. Six
turnable antagonists would make the field decorative.

### 3. Not core to the campaign

> **If their death would end the plot, they are a front, not an antagonist.**

A constraint on how they are *written*. It is why the war Corwen fought is
unnamed, why Ossa's maker is off-screen and must stay there, and why Teodor's
real culprit is a campaign decision rather than a fixture. **Every one of these
six can be removed from a campaign without the campaign noticing.**

---

## Not the hostile tier

[`../tables/roles/hostile/`](../tables/roles/hostile/) holds **10 command-tier
role templates** — bandit-captain, crime-boss, spymaster, cult-leader — for
threats you *drop in*. Those are lean generation scaffolding with no persistence.

**These six are the ones who come back.**

**Sharing a stat block across the two tiers is fine and intended.** The hostile
spec says persistence is *"none — unless they survive and start recurring, at
which point promote them."* A nemesis who is mechanically a bandit-captain is
that promotion path working. What must not be shared is the **shape**: if a
promoted hostile ends up wanting the same thing as one of the six, pick a
different axis or do not promote them.

Teodor's own scaling leans on the hostile tier explicitly — at high tier he
*hires* a `mercenary-captain`, and the captain is the encounter.

---

## Format

Same as [`../adventurers/`](../adventurers/) — frontmatter block, then
`Voice / Want / Tell` first because it is the whole point, then Actions,
Features, Equipment, `Knows` with visibility tags, Scaling, Provenance.

**Three fields only this tier has** — `grudge`, `exit`, `escalation` — plus
`grudge_seed` and the `attaches_to` / `fallback` pair, all three added during
the build:

```yaml
grudge:      null          # FILL AT CAMPAIGN CREATION — one line, party-relative
grudge_seed: "..."         # the character-level fact it hangs on. NOT a substitute.
exit:        resolved | turned | killed
escalation:  |             # what changes on appearance 2, 3, 4+

attaches_to: [<pc-slug>] | [party]     # added 2026-08-24 — see below
fallback:    "..."                     # what to do if that PC is not at the table
```

### Why `attaches_to` and `fallback` were added

**Not in the original spec, and the build needed them.** A party is 3-4 of 14
characters. Four of these six hang off a specific PC's hook, so without a
declared dependency the DM discovers at campaign creation that two of their six
nemeses are unusable.

**Every PC-dependent antagonist carries a fallback that keeps them usable
anyway.** `attaches_to: [party]` means no dependency at all — Ilma and Teodor
are portable to any composition.

⚠️ **Zephyr carries two of the six** — Maelis via the golem-body, Ossa via the
lycanthropy. A party without him drops to four usable antagonists before
fallbacks. Both fallbacks are written and both hold, but **check this first** if
Zephyr is not at the table, because it is the one composition that thins the
bench noticeably.

### Level 3, and asymmetric scaling

**All six are anchored at ~3**, because levels 1-3 is where the first playable
campaign actually runs, and a nemesis you cannot use until session twelve is a
nemesis nobody writes in.

**`## Scaling` is weighted hard toward scaling UP** — unlike the adventurers,
whose scaling is roughly symmetric. A nemesis met at 2 and still recurring at 9
has to survive a 4x power shift, and surviving it is the section's whole job.

**Note what the high-tier entries have in common:** almost none of them are about
levels. Ilma gains jurisdiction, Teodor gains a purse, Iselde gains an audience,
Ossa gains a population. **The correct tier-3 version of most of these people is
a situation the party cannot fight** — which is the honest answer to the scaling
problem rather than a stat-block arms race.

---

## Where the interactions logs live

**Not here.** These files are **template layer** — the same distinction as
`characters/` versus `LIVE/<campaign>/builds/`.

```
npcs/antagonists/<slug>.md                                   template  (this directory)
LIVE/<campaign>/canon/antagonists/<slug>-interactions.md     instance  (created at t=0)
```

**A sibling of `canon/locations/`, not inside it** — antagonists travel, and are
not bound to the place they were first met the way a captured NPC is.

Activation is a campaign-creation step: pick which of the six are live, fill each
`grudge:` against the actual party, and create the logs. See
[`../../docs/campaign-start.md`](../../docs/campaign-start.md) §5b and the t=0
manifest in §8.

---

## Provenance

Authored 2026-08-24 against the brief in `HANDOFF-v1.md` §4 Task 1 and
`npc-containers.md` §8.

**Four of six are seeded from character-level facts in the D&D Beyond JSON
audit** rather than invented — Jornis's discarded name *Zytharin*, Zephyr's
recently-contracted wereboar lycanthropy, Zephyr and Llewellyn's shared
golem-body, and Deerx's flaw verbatim. Two are party-wide and portable.

**The boundary that kept this out of front territory:**

> **Character-level facts are fair game. World-level facts are fronts.**

Jornis is Fey and hunted regardless of which campaign runs — that is true about a
*person*. *"The Sundered Choir wants to wake the thing under the barrow"* is true
about a *world*, and writing it here would be authoring a front by accident.
Every hook used passes that test; every world detail is left deliberately unnamed
for the campaign to fill.
