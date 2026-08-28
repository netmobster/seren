# gate.py — changelog

**Every change to the validator, with what prompted it.** The point of this file
is that the tool's guarantees are dated: you can tell what it was and was not
checking on the day any given ledger was written.

---

## 2026-08-28 — the verdict must match the arithmetic

⛔ **A reader downloaded the published validator and the published ledger, ran
them against each other, and found a hole in about ten minutes.**

**The gate checked that `total` rebuilt from its raw die and modifiers. It never
checked that `pass` agreed with `total` and `dc`.** All of these were accepted:

```
check   total  7  vs DC 13   pass: true     ← accepted
save    total  3  vs DC 20   pass: true     ← accepted
attack  total  5  vs AC 18   hit:  true     ← accepted
```

> ### That is the exact failure this whole project exists to exclude.
>
> **Softening a result does not require bad arithmetic.** It requires an honest
> total and a dishonest verdict — the cheapest lie available, and the one thing
> nothing was watching.

**Fixed.** `pass` is now checked against `dc`, and `hit` against `vs`. A
mismatch is refused with the arithmetic quoted back.

⚠️ **And the remediation for the previous failure was making it worse.**
`pass` is a required field on `check` and `save`, so `gate.py roll` — the
command added on 2026-08-27 so that a roll and its ledger line are one operation
— **required you to declare the outcome before the die existed.** The fix for the
lost rolls was the easiest way to write a false verdict.

**`roll` now derives `pass` and `hit` and refuses them as inputs**, the way it
already refused `roll` and `total`.

### ⭐ What the regression showed

**Every existing file still validates** — 114 entries across the played session
and the three grind probes, plus 54 facts. **No entry anywhere carried a verdict
that disagreed with its own arithmetic.**

**The hole was real and nothing had walked through it.** That is worth stating
plainly rather than either way round: the runs were honest, and the gate was not
the reason.

### Also

- `roll` and `batch` were missing from the usage banner, so the command
  described publicly as the fix for the lost rolls was undiscoverable from the
  tool itself. Added.

---

## 2026-08-27 — `roll`, `batch`, `count`

**After the first played session narrated two rolls it never wrote**, and
`check` returned *all valid* the whole time because **a missing entry is not an
invalid entry.**

- **`roll`** — produces the dice and the ledger line in one operation. An
  unlogged roll is an unrolled roll. Replaced a line in `DM.md` asking the DM to
  remember, which is not a control.
- **`batch`** — commits a whole sequence to the ledger before any of it is
  consumed, with consuming entries referencing its id. ⚠️ **The played session
  predates this and does not demonstrate it** — its eight dice were disclosed in
  the session but recorded inside a `ruling` note rather than as a `batch`
  entry. **The mechanism exists; the evidence for it does not yet.**
- **`count`** — prints entries by type and how many involved a die, because
  `check` validates shape and cannot validate completeness.

## 2026-08-27 — `facts.jsonl` validation

A second envelope: `f` ids, a required session number, and a **closed** op
vocabulary where the ledger's types are open. `append` initially could not write
the file at all — it picked its validator by filename in `scan` and not in
`append` — which made the instruction *"append every fact"* impossible as
written. Caught by the first session before play.

## 2026-08-26 — first version

Written after three grind probe runs produced 338 entries, ten of them
unreconstructable for the same reason. Validates the envelope, required and
unknown fields, enums, d20 range, dice range, and that `total` rebuilds from
`roll` plus modifiers.
