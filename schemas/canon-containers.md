<!-- Copyright (c) 2026 Jeremy Wright. All rights reserved. Published for review only; no licence granted. See LICENSE.txt -->

# canon — what is TRUE

The world model. **Not the sheet, not the state** — see
[`../docs/architecture.md`](../docs/architecture.md) §2 for that split.

Canon answers one question: *what is true about this world, and who knows it?*

---

## The visibility contract

**Every canon fact carries a visibility.** This is load-bearing, not
bookkeeping. Architecture §3:

| tag | meaning | who sees it |
|---|---|---|
| `true` | the world model | **DM only** |
| `known` | the player has learned it in play | player + DM |
| `suspected` | the player has a theory, possibly wrong | player + DM |
| `false` | the player believes something untrue | **DM only** — *and must not correct it* |

`false` is the one people delete. **Don't.** A player operating on bad
information is the good part. If the DM silently corrects a wrong belief because
nobody wrote it down as wrong, the drama evaporates and nobody can say why.

The model receives `known` + `suspected` as *what the character reasons from*,
and `true` as *what it must not contradict or reveal*. Same data, two
instructions, and they have to be labelled or the DM leaks the plot in its
narration without noticing.

---

## Structure

```
canon/
  characters/<pc>/
    bible.md       concept + voice — the source the Roleplay section draws on
    secrets.md     DM-side truth about a PLAYER character, visibility-tagged
  locations/<place>/
    state.md       what is true about this place right now
    charactermap.md  WHO IS HERE — an index, not the people themselves
  archive/         raw source captures, with provenance
```

`charactermap.md` is what keeps a long campaign inside a context window: the DM
reads the map, then loads only the people actually present.

---

## Provenance is non-negotiable

Every file here records **where it came from, when, and by what route.** A canon
fact with no source is a fact nobody can audit, and this directory is exactly
where an unsourced assertion does the most damage.

Captures land in `archive/` with their origin; derived files cite the capture.

---

## ⚠️ One open question about Ser'en

Ser'en's material was written for **Mike's campaign** — *Dark Side of the
Moonshaes*, where **Jay is a player, not the DM.** Seren is Jay's own AI-DM
system. These are not the same campaign.

So her canon is imported reference, and it forces a decision that hasn't been
made:

- **Is Ser'en a Seren PC?** Then her secrets are the DM's to run, and Seren
  gets to reveal what she is. That's a strong solo arc — the whole concept is
  *"she doesn't know what she is"*, which only pays off if someone runs it.
- **Or is she a guest sheet** imported for mechanical testing, with her real
  story belonging to Mike's table?

**Both work. They are not compatible.** If Seren runs her arc and Mike's
campaign also runs it, the reveal happens twice and the second one is dead.

> ⏸️ **Deliberately deferred, 2026-08-24.** Jay's call: *"undecided on if I play
> Ser'en or if she's the prime plot driver for the DM in the party — for now
> leave undecided as that's a runtime decision most likely."*
>
> Tracked as **SRN-3** in Currents. It also interacts with **SRN-2** (campaign
> import): if the Seren campaign turns out to be unrelated to the Moonshaes,
> the conflict with Mike's table evaporates and playing her gets much easier.

**Nothing here needs rewriting whichever way it lands** — only *who reads which
file*. `bible.md` is what she believes about herself; `secrets.md` is what's
actually true. That split is the same either way.
