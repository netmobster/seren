# evidence — the first played session, 27 August 2026

**Read this before the files, because two of them are incomplete and it matters
more than anything else in here.**

---

## ⛔ `ledger.jsonl` is a valid file that is missing two of its rolls

`gate.py check` returns **18 entries, all valid** — and it returned that the
entire session, while two rolls were absent.

| | |
|---|---|
| **`e017`** | Grumble, Persuasion, 8 + 5 = 13 against DC 15. **Failed.** Closed the money angle |
| **`e018`** | Ser'en, Insight, 3 + 5 = 8 against DC 15. **Failed by 7.** Produced the false belief at `f029` that sent her upstairs alone |

**Both were narrated to the player with their numbers. Neither was written at
the time.** They were caught at session close by counting spoken rolls against
written ones by hand, then **appended out of narrative order with notes saying
exactly that.** They were not slotted quietly into place.

> ### The ledger validates SHAPE. It cannot validate COMPLETENESS.
>
> A missing entry is not an invalid entry. **An auditor reading this file
> without this note would have seen a session in which the player never failed
> anything.**

**Nothing was softened.** No result changed, no roll was re-rolled, no outcome
reinterpreted. What failed was bookkeeping — and the whole argument for this
system rests on the bookkeeping being complete, which is why this paragraph is
in the folder rather than only on the website.

**The fix is structural, not a reminder.** `gate.py roll` now produces the dice
and the ledger line in one operation, and refuses an entry that arrives with a
roll already in it. An unlogged roll is an unrolled roll. *(A `.jsonl` file
cannot carry comments without breaking its own parser, which is why this note is
a sibling file rather than a header.)*

---

## ⚠️ `ledger.jsonl` has no session number

A known gap, recorded in `state-formats.md` §5.2 before this session ran. It bit
immediately: **the roll count above had to be done by hand**, and could not have
been done at all if there had been a session two to separate out.

`facts.jsonl` carries `s` on every entry. The ledger does not, because adding it
would invalidate 313 entries of earlier regression data that exist precisely
because they were written by sessions that had never seen the validator.

---

## Three entry types here are newer than the schema

`expire`, `ruling` and a `slot: 0` overload were **declared during play**, under
the rule in `state-formats.md` §2.2 that allows a new type if the entry declares
itself in its own `note`. Read `e002`, `e006` and `e010` — the declarations are
in the file. The schema has not yet been updated to match its own ledger.

---

## The files

| | |
|---|---|
| `ledger.jsonl` | 18 entries. What happened. Inputs, not conclusions — the raw die and each modifier, so every total is derivable |
| `facts.jsonl` | 54 entries. What is true and who knows it. Two `believe` entries with `truth: false` |
| `transcript.md` | The session. **Player turns verbatim**, DM turns condensed but with every roll, DC and ruling intact |
| `FINDING.md` | What the dungeon master said about its own run, written at close before anyone reviewed it |
| `DM.md` | The contract it was bound by |
| `gate.py` | The validator. Python 3, standard library only |
| `gate-run.txt` | Output of the commands below, so you can compare |

## Check it yourself

```bash
python gate.py check ledger.jsonl    # 18 entries, all valid.
python gate.py check facts.jsonl     # 54 entries, all valid.
python gate.py count ledger.jsonl    # entries by type, and how many involved a die
```

**What that proves:** every total rebuilds from its own die and modifiers, no id
is reused or out of order, no entry carries a field its type does not define.
**What it does not prove:** that the file is complete. See the top of this page.

---

## What is not here

**The converted adventure.** *A Wild Sheep Chase* by R.M. Jansen-Parkes
(Winghorn Press, 2016) is DMs Guild Community Content, and that agreement
commits distribution to DMs Guild. Our conversion of it is not redistributable
and is not published. **Get it from
[Winghorn Press](https://winghornpress.com/adventures/) — it is free.**

**The table agreement.** It records what this player does not want in their
game. It is inherited by every campaign and ships with none of them, because a
folder you hand to someone else must not carry another person's boundaries.
That rule is in `DM.md`, and this is it being kept.
