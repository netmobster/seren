<!-- Copyright (c) 2026 Jeremy Wright. All rights reserved. Published for review only; no licence granted. See LICENSE.txt -->

# Campaigns

**This directory holds TEMPLATES. A played campaign does not live here.**

```
campaigns/
  modules/<slug>/    an adventure converted to schema · portable · MAY SHIP
  candidates/        adventures under consideration
  reference/         third-party source text · ⛔ never committed
```

> ### ⛔ THE PLAYTHROUGH LIVES IN `LIVE/<campaign>/` — corrected 2026-08-27
>
> **This README described the instance tree as `campaigns/<name>/` until
> today.** [`../LIVE/README.md`](../LIVE/README.md) is the authority:
>
> ```
> campaigns/modules/<slug>/   template · portable · MAY SHIP
> LIVE/<campaign>/            instance · yours   · NEVER SHIPS
> ```
>
> ⚠️ **A campaign folder here would ship with the repo.** `.gitignore`
> excludes `LIVE/*` and has never excluded anything under `campaigns/`.
>
> ⭐ **Four documents described that tree and no two agreed.** SRN-42. The
> canonical shape is [`../docs/campaign-start.md`](../docs/campaign-start.md)
> §1 — **this file no longer restates it**, per the rule that nothing holds
> state another file maintains.

**A campaign is an instance.** The masters in
[`../characters/`](../characters/) and the world in [`../npcs/`](../npcs/) are
shared; a campaign binds them to a level, a map, a set of fronts, and a
history — **in `LIVE/`.**

---

## The three kinds of DM knowledge

Keeping these separate is what stops the DM either railroading or improvising
mush. They differ by **commitment** and **attachment**:

| | committed? | attached to? | behaviour |
|---|---|---|---|
| **fronts.md** | ✅ yes | a faction | **advances on its own clock** whether or not the player engages |
| **secrets.md** | ✅ yes | one character or NPC | true *now*, hidden from the player |
| **ideas.md** | ❌ **no** | nothing yet | **does not exist** until a matching thread opens |

An idea is not yet true. That's the point — it costs nothing to hold a hundred
of them, and none of them constrain the world until one is spent.

---

## ideas.md — the improv bank

The failure mode of an idea list is that it becomes a graveyard nobody reads
mid-session. Two rules prevent that:

**1. Every idea records its TRIGGER.** Not "what it is" — *"what would have to
happen at the table for this to fit."* The DM doesn't browse the list; it gets
retrieved when a thread matches.

**2. A spent idea is promoted, not ticked off.** The moment it enters play it
stops being an idea and becomes a **front** (if it's now in motion) or **canon**
(if it's now just true). Delete it from `ideas.md` in the same breath. An idea
left in the pool after being used will get introduced twice.

### Entry format

```markdown
### <short name>
**Trigger:** the kind of thread that makes this fit
**Hook:** one or two sentences — what the player actually encounters
**Cost:** what it commits the world to, if spent
**Source:** where it came from (a character sheet, a session, invention)
```

**Cost** is the field people skip and shouldn't. Some ideas are free scenery.
Others, once introduced, permanently change what the setting is. Knowing which
before you spend it is the whole discipline.

---

## Where ideas come from

Three feeds, in descending order of quality:

1. **Unexplained things already on the character sheets.** The strongest ideas
   are the ones the players *already made true* without meaning to. See
   [`IDEAS.md`](IDEAS.md) — the seed pool is entirely of this kind.
2. **Threads the players open and walk away from.** Anything a player asked
   about once and then dropped is pre-validated interest.
3. **Invention.** Cheapest to produce, weakest to land, because nothing in the
   fiction is already pointing at it.

---

## If Seren ever goes public

**Decided 2026-08-24 (Jay). Not in scope — recorded so the decision isn't
re-litigated later, and so nothing gets built in a way that forecloses it.**

> ### The schema ships. The adventures we ran do not.

Two artifacts, and only one of them is ever distributable:

| | what it is | ships? |
|---|---|---|
| **the schema** | the module format, the campaign folder spec, `campaign-start.md` and its conversion step, the container and antagonist formats | ✅ **yes** — entirely ours, no third-party content in it |
| **a module we derived from someone's adventure** | Welton, or any other published one-shot rendered into our format | ⛔ **never** |

**A derived module is not ours to publish**, regardless of how freely the
original was given away. Free to download and run is not free to redistribute in
a new wrapper, and *"we reformatted it"* is not a defence anybody should want to
make. **This is not a licence-risk calculation. It is not okay, and that's the
end of it.**

### What goes out instead

**An original sample one-shot**, written by us, in the format — so that anyone
adopting the schema has a worked example to read and something to play on day
one. A format without a filled example is not adoptable.

**That costs less than it sounds.** Seren already holds 42 role templates, 6
antagonists, 26 homebrew feat shapes, 10 item shapes, and an idea pool harvested
from real character sheets. A sample module is assembly from parts we own, not
authorship from nothing.

### What this means for anyone building now

Nothing changes in how work proceeds, with one exception:

**Keep the format and the instances in separate directories from the start.**
`campaigns/modules/` is the format's home; a specific playthrough lives
elsewhere. If a derived module ever sits in the same tree as the shippable
schema, someone eventually publishes it by accident — and the fix is a directory
choice today versus a migration and an apology later.

**If we ever do want to ship a Welton module, the answer is to ask its author.**
Richard Jansen-Parkes, one person, contact address on
[his About page](https://winghornpress.com/winghorn-press-about/), explicitly
open to collaboration. A conversation, not a workaround.
