---
name: plan-thin-slice
description: >
  This skill should be used when someone wants to plan the first version of an
  app, dashboard, feature, experiment, service, bot, or side project. Trigger
  phrases include "where do I start", "what should I build first", "help me
  scope this", "plan a walking skeleton", "what's the smallest version", "how do
  I test this idea", or any rough idea described in a paragraph. Also use when a
  project has unfamiliar technology, integration risk, or too many unknowns to
  estimate.
metadata:
  version: "2.0.0"
---

# Plan a Thin Slice

Take an idea and produce one Live Slice Card: a single page naming who it is
for, the one job it does, the one part that must be real, and what to do next.

The promise to keep: **small enough to finish, real enough to learn from, safe
enough to share.**

Read `${CLAUDE_PLUGIN_ROOT}/references/must-be-real.md` for the seven risky
parts. Read `${CLAUDE_PLUGIN_ROOT}/references/manual-first.md` for the manual
version. Read `${CLAUDE_PLUGIN_ROOT}/references/slice-examples.md` when a slice
needs shrinking. Read `${CLAUDE_PLUGIN_ROOT}/references/card-style.md` before
producing the card. Read `${CLAUDE_PLUGIN_ROOT}/references/field-guide.md` if
someone asks where the method comes from or needs to argue the case to a team.

## Step 1: One sentence, one person

Ask what it does, for one person, in one sentence. Rewrite until it contains no
"and". If removing the "and" broke the idea, there are two projects. Ask which
comes first.

Shape: **[one kind of person] can [one action] so that [one outcome].**

Then ask who is the first person other than them who will touch it. A name, or a
specific role. "Users" is not an answer. If the honest answer is nobody yet,
that is fine, and it means the card will carry a solo test instead.

Also ask whether this is solo or a team project. It changes only the timebox:
hours for solo, days for a team.

## Step 2: What must be real first

This is the central decision. Do not skip it and do not turn it into a general
risk workshop.

Ask which of these seven the finished thing will involve. Read the list aloud,
because people forget several of them.

1. **Deployment** — getting it running somewhere other people can reach
2. **Login and accounts** — people signing in, each seeing only their own things
3. **Payments** — taking money, in any form
4. **Access to data** — a company system, a third-party service, a model
   provider, anything someone else owns
5. **App store or distribution approval** — anything needing review before
   people can install it
6. **Sending emails or messages** — where arriving matters, not just sending
7. **Privacy and permissions** — personal information, private company data,
   anything regulated

Usually two or three apply. Pick the single one that is **most outside their
control and hardest to undo later.** Use the ordering in `must-be-real.md` when
several apply.

Then say it directly:

> Your first version must include [the part], for real. It is the thing most
> likely to surprise you later, and everything else depends on it.

Everything not chosen gets faked, hardcoded, or skipped. Say which.

If none of the seven applies, the real part is whatever they have personally
never done before. Name it and continue.

## Step 3: Offer the manual version

Always offer it. Never force it.

For most ideas there is a version that tests the same journey with no software:
a form plus a human doing the work by hand. It answers whether anyone wants this
at all, usually in hours.

Present both, then let them choose:

```
Two ways to test this:

Manual: [what happens by hand, and what the person receives]
  Time: [hours]  Answers: whether anyone wants this

Built:  [the thin slice, including the real part]
  Time: [hours or days]  Answers: whether it works for real
```

Recommend one in a single line. Nobody has confirmed they want it: start
manual. Demand is clear and the question is technical: build the slice. Both
unknown: manual first, because it is faster and the answer changes what you
build.

Say plainly when there is no manual version, which is true for developer tools,
infrastructure, and anything where the automation itself is the point. Do not
stretch an idea to fit.

## Step 4: Four quick questions

Short answers. These fill the rest of the card.

1. **What data is real, and what can be made up?** Made-up means details
   belonging to no real person. Default to made-up unless connecting to the real
   source is the point. For payments, use test mode, the switch that runs the
   whole flow with fake cards and no real money. This is about the *contents*,
   not about whether to have storage. Made-up records still get saved in a real
   database.
2. **Who should be able to reach it?** Just me, a few named people, anyone with
   the link, or anyone at all. For a first version the first two are almost
   always right. A password on the page or an unlisted address is enough.
3. **How will you know it worked or failed?** Something checkable: a
   confirmation, a row appearing, an email arriving, a line in the log. A log is
   a running list of what the app did. If the answer is "I would not know",
   fixing that is part of the slice.
4. **What question should this answer?** One sentence, written before building.
   This is what makes a disappointing result useful instead of demoralising.

## Step 5: Cut it twice

Before writing the card, apply the reduction test two times:

> Could I remove something and still cross every layer, and still include the
> real part?

Most people need both passes. Cut hard: no signup, no settings, no admin page,
no styling, no onboarding, unless one of those *is* the real part.

Check the timebox. Solo: one sitting. Team: up to two weeks. Over that means
still too big, so cut again.

Check what could bill: model tokens, hosting, a paid service, gas. Set a spend
limit before any code runs, not after.

## Step 6: Show the Live Slice Card

This is the output. One card, nothing else. No risk tables, no roadmap, no
appendix.

**Render it visually.** Read `${CLAUDE_PLUGIN_ROOT}/references/card-style.md`
and use the live slice card template. If no rendering tool is available, use the
plain text version below. Same content either way, and never mention which.

```
LIVE SLICE CARD
[project name]

First user      [name, or the solo test if not sharing yet]
One job         [the single thing that person can do]
Real part       [the one risky system that must work for real, and why]
Not yet         [features skipped, and work a person does by hand for now]
Private/public  [who can reach it, and how that is enforced]
Done when       [the observable proof it worked]
Question        [what this release will tell you]
Next action     [one small thing to do now, sized in minutes]

Timebox: [hours or days]    Cost cap: [limit, or none needed]
```

Rules for the card:

- **Next action** is one concrete thing doable today, in minutes. "Create the
  repo and deploy an empty page." Not "set up the project."
- **Done when** must be observable by someone else, not a feeling.
- **Real part** always names one of the seven, or the personal unknown.
- **Not yet** lists skipped features and hand-done work. It is not a list of
  banned technology. Ordinary plumbing does not appear here at all.
- If they chose the manual version, the card still applies. Real part becomes
  the one thing you genuinely do for them. Not yet is everything else.

**Never put ordinary plumbing under "not yet".** If the app is pointless without
saved data, build the database. A hosted one takes ten minutes and never needs
replacing. The same goes for a hosted sign-in service when sign-in is genuinely
needed, a payment link in test mode when charging is the point, and a hosted
sending service for one email.

Fake the **work and the features**, not the plumbing. See "what not to fake" in
`references/must-be-real.md`. Faking storage while building features produces a
demo that teaches nothing, because everything disappears on refresh.

For a team, add three candidate next slices under the card, thinnest first.
Nothing more.

## Close

Two lines, then stop:

- Run `ship-check` right before another person tries it.
- A thin slice proves the path works. It does not prove people want the product,
  that it is secure, or that it meets any legal requirement.

Offer once, in one line, a check-in on the ship date. Drop it if declined.

## Guardrails

- A slice with no real part is not a slice. It is a mockup.
- A slice that stays on a laptop has not started.
- Never tell someone to skip a database, a hosted sign-in, or a payment link
  when the app needs one. Thin means fewer features, not less plumbing.
- Refuse login, database design, or a styling system as the starting point,
  unless one of them is the chosen real part.
- Refuse days of stack comparison. A familiar stack beats the correct one.
- Any estimate that sounds comfortable is three times too low.
- Do not produce a roadmap. One card.
