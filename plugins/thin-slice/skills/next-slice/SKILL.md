---
name: next-slice
description: >
  This skill should be used when something is already live, even barely, and the
  person asks "what do I build next", "what's the next step", "how do I sequence
  this", "what should I do this weekend", or has a wishlist and cannot decide
  what comes first.
metadata:
  version: "2.0.0"
---

# Next Slice

Pick one next thing, make it smaller than they expect, and hand it back as a
card.

The rule underneath: **it stays live and working at every step.** No long
branch. No slice that is a big switch-over at the end.

Read `../../references/must-be-real.md` if a part of the system
is still faked and it is time to make it real.

## Step 0: Ask what changed

Read `../../references/working-on-a-live-project.md` first.

People do things between messages without narrating them. They sign up, connect
accounts, get approvals, and swap test data for real data, and none of it
appears in the conversation. Whatever you remember about this project is the
state at the last thing you were told, which is not the current state.

Three questions, before anything else:

1. What have you set up, installed, or connected since we last spoke?
2. Has anything on the "not yet" list become real?
3. Is any of the data real now, rather than test data?

If the answer to 2 or 3 is yes, the card changed. Update it before sequencing
anything, because "not yet" and "private or public" are both probably wrong now.

## Step 1: Confirm it is live

Ask whether someone who is not the builder can reach it right now. If not, stop
and route to `plan-thin-slice`. Sequencing on something that has never run end
to end is planning on a guess.

If it used to be live and is broken now, fixing that is the next slice. Nothing
else.

## Step 2: Check whether a small fix comes first

Before touching the wishlist, three quick questions:

- **Safety.** Is real personal information, customer data, or a secret key
  exposed or stored without need? Is it open to more people than intended?
- **Reliability.** Has it broken since going live? Could it fail without telling
  anyone?
- **Learning.** Can you tell whether people use it and whether the main action
  succeeds? Did the last release answer its question, and were its "done when"
  conditions actually met rather than just attempted?

If any turns up something, that is the next slice, ahead of any feature. Keep it
small: swap real names for made-up ones, add a password to the page, move a key
into the hosting settings, add one line recording whether the action worked.
Each is under an hour.

If nothing turns up, say so in one line and continue. Usually nothing does.

## Step 3: Sort the wishlist

Ask for everything it should eventually do, messy version. Sort each item into
one bucket:

| Bucket | Meaning |
| --- | --- |
| **Safer or more reliable** | Protects information, limits access, stops silent failures |
| **Makes it real** | Without this, nobody can use it for its actual purpose |
| **Easier to learn from** | Lets you see whether it works and whether people use it |
| **Nicer** | Improves something that already works |
| **Bigger** | New capability beyond the original one sentence |

Work in that order. Nothing from "nicer" or "bigger" until the first three are
empty.

Two things usually become obvious: "makes it real" is small, and most of the
wishlist is "bigger".

When "makes it real" empties, say so explicitly. People cross the line from
unusable to usable without noticing, and keep building instead of showing
anyone.

## Step 4: Is it time to make a fake part real?

The first slice deliberately faked things. Some of those fakes are now the
constraint, and some are still fine for months.

Ask which fakes are still in place. For each, one question: **is this costing
you anything yet?**

- A person doing a step by hand, and it takes ten minutes a week: leave it
- The same person spending two hours a day: automating it is the next slice
- Made-up data, and nobody has asked for real data: leave it
- Hardcoded values that block the next real user: replace them

A cheap manual step that works is not debt. The failure is never deciding, not
the fake itself.

## Step 5: Rewrite as one action, then halve it

Write the chosen item as **[actor] can [action] and [observable result].**

Reject anything shaped like "build the database schema", "build the API" or
"refactor the components". Those are layers, and building by layer pushes all
the joining-up risk to the end. Name them and rewrite them.

Then cut it:

- Can it work for one case instead of all cases?
- Can the input stay hardcoded one more round?
- Can it be ugly?
- Can the error case just fail loudly for now?
- Can it work for internal users only, behind a switch?

If it does not fit the timebox, cut again.

## Step 6: Output

One short card. Nothing else.

**Render it visually.** Read `../../references/card-style.md`
and use the live slice card template with these rows only. If no rendering tool
is available, use the plain text version below.

```
NEXT SLICE
One job         [actor can action, observable result]
Real part       [what becomes real this time, or "nothing new"]
Not yet         [what stays skipped or hand-done]
Done when       [observable proof]
Question        [what this tells you]
Next action     [one thing to do now, in minutes]

Timebox: [hours or days]
```

If Step 2 found something, say clearly that this slice is a small fix rather
than a feature, and frame it as protecting the work already done.

For a team, add the ranked list of what comes after. For a solo project, stop at
the card. A side project with a roadmap has usually stopped being fun.

## Guardrails

- One slice at a time. Never a plan for the next five weekends.
- Refuse rewrites, refactors and stack migrations unless something is broken.
  "The code is messy" is not a next slice.
- Refuse anything that takes it offline while in progress.
- Refuse big switch-overs. Split them.
- If the same item has been "next" three times and never happened, it is too
  big, too boring, or the project changed. Ask which.
- If it has been usable a while and nobody has seen it, say so. The next slice
  might be telling one person about it, then `ship-check`.
