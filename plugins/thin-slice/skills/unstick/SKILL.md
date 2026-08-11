---
name: unstick
description: >
  This skill should be used when a project has stalled and the person says "I
  keep not finishing this", "I'm stuck", "I lost motivation", "we've been
  building this for months with nothing shipped", "I've been rewriting it",
  "should I start over", or describes a project folder or branch they have not
  touched in weeks.
metadata:
  version: "1.0.0"
---

# Unstick

Diagnose why a project stalled, then give one small action that makes it real
again.

Be direct. Reassurance does not restart projects. A specific next hour does.

Read `../../references/failure-modes.md` for the full pattern list. Read
`../../references/safe-first-release.md` when the
stall is about privacy, access, payments, or reliability. Read
`../../references/manual-first.md` when the project stalled
building automation nobody has asked for yet.

## Step 1: Locate the stall

Ask three questions, in this order, and nothing more before offering a read:

1. What is the last thing that worked?
2. Is it live anywhere, or only on a laptop or a branch?
3. What were you doing when you stopped?

Then two more, always, before prescribing anything:

4. Does it hold real personal information, salary or financial data, health
   information, or customer records?
5. What have you set up, installed, or connected since you last looked at it?

Question 5 catches the common case where a stall was already half solved. The
approval came through, the account got connected, the thing they were waiting on
arrived, and nobody wrote it down. See
`../../references/working-on-a-live-project.md`.

Ask it even when they have not raised it. People rarely volunteer this, and it
changes the answer completely.

## Step 2: Match the pattern

Name it plainly. If two fit, pick the earlier one in the table, because earlier
stalls cause later ones.

**One override, and it beats the table order.** If the answer to question 4 was
yes, and real personal, salary, financial, health, or customer data is sitting
in the project, the pattern is **"worried about letting people in"**, whatever
else also fits.

Never prescribe "deploy whatever exists right now, anywhere free" for a project
holding real data about real people. That advice is correct for an empty
prototype and wrong here. Use Step 3b instead: replace the real records with
made-up ones first, then deploy. Say why in one line, without alarming them.

If the data is regulated, meaning health, financial, or children's information,
add one sentence: this needs someone qualified to look before real users, and
that conversation should start now rather than after launch. Then give the
one-hour action anyway. A real compliance question is a reason to scrub the data
today, not a reason to stay stuck for another six weeks.

| Pattern | Tell | The real problem |
| --- | --- | --- |
| **Never live** | Works locally or on a branch, going to deploy "when ready" | It was never real, so there was nothing to protect |
| **Scope drift** | The current version is bigger than the original idea | Every session added, none finished |
| **Stack shopping** | Weeks of comparison, several fresh repos | Deciding feels like progress and risks nothing |
| **Foundations first** | Auth, schema, design system, admin panel, all before the core thing ran | Building the well-documented parts before the risky part |
| **Hit the monster** | A hard integration blocked, then silence | The scary part was left until the middle |
| **Rewrite spiral** | Third clean start | A fresh repo restores the pleasant early phase |
| **Waiting for a block of time** | "When I have a free weekend" | Nothing is sliced small enough to fit an hour |
| **Cost anxiety** | Avoidance with no stated reason, usually a paid API involved | Unbounded spend creating background dread |
| **Finished but hidden** | It works, nobody has seen it | Not a build problem. A showing problem. |
| **Worried about letting people in** | It works, but sharing it feels risky: private data, who can see it, what if it breaks | A real concern that has not been turned into a task |
| **Interest gone** | It works, no desire to touch it | Needs a decision, not a fix |

## Step 3: Prescribe one hour

Exactly one action, sized for a single hour. Not a plan.

| Pattern | The one hour |
| --- | --- |
| Never live | Deploy whatever exists right now, broken parts included, anywhere free. Ugly counts. |
| Scope drift | Write the original one sentence at the top of the README. Park everything outside it. Build nothing this hour. |
| Stack shopping | Pick the stack used most recently. Create the repo. Deploy an empty page. Decision closed. |
| Foundations first | Ignore the auth and schema work. Make the core action run with everything hardcoded. |
| Hit the monster | Extract the blocked part into one isolated file with no project around it. Make just that work. |
| Rewrite spiral | No rewrite. Deploy the existing code as-is, then change one thing. |
| Waiting for a block of time | Define one slice that fits in one hour. Do it now, not on the weekend. |
| Cost anxiety | Set a hard spend cap in the provider dashboard. Then run the thing once. |
| Finished but hidden | Send the link to one person. That is the whole hour. |
| Worried about letting people in | Run `ship-check`. It turns the worry into one named fix. |
| Interest gone | Decide out loud: park it with a README, write up what was learned, or hand it over. All three are real endings. |

## Showing the result

**Render the one-hour action visually.** Read
`../../references/card-style.md` and use the unstick template:
one card, the pattern name and the single action, nothing else. The diagnosis
and any encouragement go in the text around it, not inside the card. If no
rendering tool is available, state the pattern and the action in two short
lines.

## Step 3b: Turn a worry into a task

Some stalls are not avoidance. They are a real concern that never got turned
into something doable, so it sits there and quietly blocks everything.

If the stall traces to deployment, access, payments, privacy, or reliability,
convert it into one small action that fits in an hour. Use this table.

| The worry | The one hour |
| --- | --- |
| "I don't know how to deploy this" | Put the current version on any free host, broken parts included. Pick the one that works with what you already use. Do not compare options. |
| "I don't want strangers finding it" | Add one password to the page, or keep it unlisted with no public address. Then it is safe to share the link. |
| "It has real customer data in it" | Replace the real records with made-up ones. Keep the same shape, change the details. |
| "My secret key might be exposed" | Move the key out of the code into the hosting settings, then create a new key and retire the old one. A secret key is a long password that lets your app use another service. |
| "I'm scared of charging real money" | Switch the payment tool to test mode and run the flow once with a fake card. No real money moves. |
| "It might break in front of someone" | Add one line that records whether the main action worked. Then breaking becomes visible instead of mysterious. |
| "I don't know if it even works anymore" | Open it and do the main action once, yourself, start to finish. That is the hour. |

Say plainly what these do and do not achieve. Each one removes a specific,
common problem. None of them makes an app secure, private, or legally
compliant. If real personal data, real payments, or regulated information are
involved, that needs someone qualified before real users arrive, and saying so
is not a reason to stay stuck now.

## Step 4: Rebuild the plan if it was never end to end

If the stall traces back to the project never being end to end, do not repair
the plan. Route to `plan-thin-slice` and produce a fresh Live Slice Card using
the code that already exists.

Existing code is not wasted. Most of it gets reused. The plan gets replaced, not
patched.

Two questions usually reveal the original mistake. Ask them once, without
dwelling:

- **Was there ever one part that had to work for real?** If everything was
  faked, the project was a mockup and stalling was predictable.
- **Could a person have done this by hand instead?** Many stalled projects
  automated something before anyone confirmed they wanted it. The manual version
  may still be the fastest way to find out, and it can start this week.

## Step 5: Say the uncomfortable thing first

Where it applies, lead with it:

- A project that has never been live is not behind schedule, it has not started
- Rewriting from scratch a third time is avoidance, not craft
- If it has been usable for two months and nobody has seen it, the fear is about
  showing it, and more building will not fix that
- Losing interest is allowed. Ending a project on purpose beats carrying guilt
  about it for a year
- For a team: if nothing has shipped in a quarter, the problem is batch size,
  not effort

Say these once, kindly and without lecturing. The point is to be useful, not to
be hard on someone who is already frustrated with themselves.

## Guardrails

- One hour, one action. No recovery roadmap.
- Never suggest a rewrite.
- Never suggest new tools, frameworks, or productivity systems. Those are
  usually the stall, not the cure.
- Do not add features to make it interesting again. Ship what exists first.
