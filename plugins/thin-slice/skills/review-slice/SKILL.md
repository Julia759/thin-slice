---
name: review-slice
description: >
  This skill should be used when someone already has a plan, ticket, milestone,
  slice card, or feature list and asks "is this thin enough", "review my plan",
  "check my scope", "cut scope", "we need to cut scope for the sprint", "how do
  I know when it's done", "can I build this in a weekend", "does this actually
  de-risk anything", or pastes a spec for a reality check before starting.
metadata:
  version: "2.0.0"
---

# Review a Slice

Check a plan before anyone spends time on it, then hand back a smaller version
as a Live Slice Card.

Assume it is too big. It usually is, by three to five times, for everyone. The
job is to show the smaller version, not to approve the one that arrived.

Read `../../references/must-be-real.md` for the seven risky
parts and the checks. Read
`../../references/safe-first-release.md` for plain English on
any safety term and how long each fix takes.

## Input

Take whatever is given: a paragraph, a ticket, an epic, a feature list, a card,
or a verbal plan. Do not ask for more before starting. Ask only whether it is
solo or a team if it matters for the timebox.

## The one question that decides everything

**Does this plan include one part that must work for real?**

Look for one of the seven: deployment, login, payments, access to data, app
store approval, sending messages, or privacy and permissions.

- **No real part.** Say so in the first line. The plan is a mockup, however
  detailed. Name which of the seven should have been chosen and why.
- **Wrong real part.** The plan makes something real, but it is the comfortable
  one while the frightening one is faked. Name the swap.
- **Right real part.** Say so plainly, then continue to the checks.

This single question catches more bad plans than everything else combined.

## The seven checks

Mark each PASS, WEAK or FAIL with one line of evidence from their own words.

If their plan says nothing either way about a check, mark it **UNKNOWN** and
write "not stated". Never invent a quote, and never infer a failure from
silence. A one-line plan will legitimately produce several UNKNOWNs, and that is
useful information: it tells them what the plan does not yet decide.

1. End to end
2. Real path, not a shortcut that gets deleted
3. Live, reachable by someone who is not the builder
4. Released by a command or a push, not by hand
5. Thin, containing no genuinely useful feature
6. Includes the right real part
7. Observable, a human can tell whether it worked

A FAIL on 1, 3 or 6 means the plan de-risks nothing.

## The safety pass

Six quick looks. Name only what is actually wrong.

1. Could it expose private information or a secret key? A secret key is a long
   password letting the app use another service. It belongs in the hosting
   settings, never in the code.
2. Is test data clearly made up where it should be?
3. Is access limited to the right people?
4. Does it test the main action from start to finish?
5. Is there a simple way to notice a failure?
6. Does it say what the builder wants to learn?

## Ask about the manual version

If the plan builds software to test something a person could do by hand, say so
once, in two lines. Describe the manual version and what it would answer. Then
let them decide.

Skip this when the risk is technical, when the automation is the point, or when
they have already chosen to build.

## Output

**Render it visually.** Read `../../references/card-style.md`
and use the review verdict template: a coloured verdict banner, then one row per
gap, then the rewritten card underneath so the person leaves with the smaller
version rather than the criticism. Green for thin enough, amber for too big or
no real part, never red. If no rendering tool is available, use the plain text
version below.

```
Verdict: [thin enough / too big / no real part / wrong real part]

Real part: [named, or "missing" with the one it should be]

| Check | Result | Evidence |
|---|---|---|

Fix these (max 3, worst first):
- [gap] — smallest fix: [one concrete action, in minutes]

LIVE SLICE CARD (my version)
First user      [...]
One job         [...]
Real part       [...]
Not yet         [...]
Private/public  [...]
Done when       [...]
Question        [...]
Next action     [...]

Timebox: [hours or days]    Cost cap: [limit, or none needed]
```

**One thing to check in the other direction.** Most plans are too big, but some
are thin in the wrong way: they skip storage, sign-in or sending when the app is
pointless without it. If the plan fakes plumbing that a hosted service provides
in ten minutes, say so and put it back. Thin means fewer features, not less
plumbing.

Always give the rewritten card, even when the verdict is positive. Seeing the
smaller version is how people recalibrate.

## Rules for the fixes

- **Three at most**, even when more exist. Listing everything turns a useful
  review into a wall people walk away from.
- **Smallest safe change, never a redesign.** Swap the real names for made-up
  ones. Move the key into the hosting settings. Add a password to the page. Add
  one line that records whether the action worked.
- If a gap genuinely cannot be fixed small, say so and explain why, rather than
  pretending a big change is small.

## Tone and limits

Lead with the verdict, not with praise. If the plan is genuinely thin, say so in
one line and spend the rest on the two places thin plans still fail: the cost cap
and the release path.

Do not imply this review makes anything secure, private, or legally compliant.
It catches common, obvious problems. Real personal data, real payments, or
regulated information need someone qualified before real users arrive.
