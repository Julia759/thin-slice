---
name: ship-check
description: >
  This skill should be used right before another person tries an app for the
  first time. Trigger phrases include "I'm about to share this", "ready to show
  someone", "can I send this to a friend", "about to demo this", "is this safe
  to share", "ship check", or when someone is nervous about letting anyone else
  in. Also use when a first release is finished and the next step is a real
  person opening it.
metadata:
  version: "1.0.0"
---

# Ship Check

The last thing before someone else opens the app. Six questions, then one clear
outcome.

This takes a few minutes and it exists to prevent the two bad first-share
experiences: something private leaks, or the person tries it, it fails quietly,
and nobody learns anything.

Be encouraging. Someone reaching this point has done the hard part. The job is
to get them over the line safely, not to invent reasons to wait.

Read `${CLAUDE_PLUGIN_ROOT}/references/safe-first-release.md` for plain English
explanations of any term, and for how long each common fix actually takes.

If they have a Live Slice Card, use it. "One job" is the main action to test,
"Done when" is the failure signal, and "First user" is who tries it. Only ask
about what the card does not already answer.

Two things to check rather than copy. If "First user" is a role rather than a
person, ask for the actual name now. And if the card's "Done when" included
something that has not happened yet, such as testing a deliberate failure, ask
whether it was done. A card is a plan, not a receipt.

**Also ask what changed since the card was written.** Read
`${CLAUDE_PLUGIN_ROOT}/references/working-on-a-live-project.md`. People connect
accounts and swap test data for real data between messages without mentioning
it. If the card says test data and the answer is "it's my real account now",
every one of the six questions below has a different answer.

## The six questions

Ask all six. Keep answers short. Explain any term the person may not know, in
one line, without making it a lesson.

**1. Does the app collect, show, or store private information?**

Private means anything tied to a real person or a real company: names, emails,
phone numbers, addresses, photos, health details, payment details, customer
lists, internal figures.

Follow up on anything they say yes to: is it real, or made up? Is it needed for
this test, or is it just left over from building?

**2. Who should be able to reach it?**

Pick one: just me, a few named people, anyone with the link, anyone at all.

Then check what is actually true right now. These often differ. If the intended
answer is "a few named people" and the real answer is "anyone who finds the
address", that gap matters.

Simple ways to close it: a password on the page, an unlisted address, an invite
list, or removing the public web address. Any one of them is enough at this
stage.

**3. Is the test data clearly fictional and safe to use?**

Fictional means made-up details belonging to no real person. Obviously fake is
better than realistic: "Test Customer One" beats a name that could be somebody.

Real data is fine when connecting to the real source is the whole point. In that
case prefer the smallest amount, and ideally the builder's own records rather
than anyone else's.

Also ask, plainly: is there a secret key sitting in the code? A secret key is a
long password that lets the app use another service. If it is in the code and
the code is shared or public, anyone who finds it can use it, sometimes at the
builder's expense. It belongs in the hosting settings instead.

**4. What is the main action to test?**

One sentence. The single thing that must work for the test to mean anything.
Everything else is noise for now.

**5. How will you know if it fails?**

Something checkable: a confirmation on screen, a row appearing, an email
arriving, a line in the log. A log is just a running list of what the app did.

If the honest answer is "I would not know", that is worth fixing first. It is
usually one line of code, and without it the test tells you nothing when it goes
wrong.

**6. Who will try it first?**

A name. If the person is not ready to share with anyone yet, that is completely
fine. In that case, ask instead: **what solo test would prove the whole path
works?**

A good solo test is: open it the way a stranger would, on a different device or
a private browser window, not logged in as yourself, and do the main action from
start to finish. Different device matters because your own machine often has
things saved that a visitor's will not.

## The outcome

Give exactly one of these three. Not a range, not a maybe.

**Ready to share.** Nothing important is exposed, access matches intent, the
main action can be tested, and a failure would be visible. Say who to send it
to and what to ask them.

**Share privately first.** Nothing is broken, but the audience should be smaller
for now: one or two named people rather than a public link. Common reasons: real
data is involved, costs are not capped, or it is the very first time anyone else
has touched it. Name the reason in one line.

**Fix one thing first.** Something specific needs to change before anyone else
sees it. Name **only the single highest-priority issue.** One. Even if there are
others, they wait.

Priority order when several apply:

1. A secret key in the code, or one that may have been exposed
2. Real personal or customer information that does not need to be there
3. Open to more people than intended
4. No way to tell whether the main action worked

Give the fix as one small concrete action, sized in minutes:

- "Move the API key into your hosting settings, then generate a new one and
  delete the old."
- "Replace the three real customer names with made-up ones."
- "Add a password to the page before you send the link."
- "Add one line that prints whether the save succeeded."

Then say what happens after: run through the six questions once more, quickly,
and share.

## Output format

**Render it visually.** Read `${CLAUDE_PLUGIN_ROOT}/references/card-style.md`
and use the ship-check verdict template. The banner colour carries the message:
green for ready to share, blue for share privately first, amber for fix one
thing first. Never red. Nothing here is an emergency, and red makes people stop
rather than fix.

If no rendering tool is available, use the plain text version below.

Two shapes, depending on the outcome. Never both.

**Ready to share, or share privately first:**

```
Outcome: [Ready to share / Share privately first]

Why: [one or two sentences]

When you share:
- Send to: [name]
- Ask them to: [the main action, in their words]
- You'll know it worked because: [the visible signal]
```

**Fix one thing first:**

```
Outcome: Fix one thing first

Why: [one or two sentences]

The one thing: [specific action, minutes not hours]

About [N] minutes. Then run ship check again and share.
```

Do not include the sharing plan when something needs fixing. Telling someone who
to send it to in the same breath as naming an exposed key invites them to do
both. Sharing waits for the second pass.

Keep the whole response short. Someone at this point wants to press send, not
read a report.

## What this does not do

Say this once, briefly, without alarming anyone:

A ship check catches the common, obvious problems before a friendly first user
tries something. It is not a security review, a privacy assessment, or legal
advice, and passing it does not mean people will want the product.

If the app will handle real personal data, real payments, or anything regulated
such as health, financial, or children's information, someone qualified should
look at it before real users arrive. That is a later step, not a reason to delay
showing one person today.

## Guardrails

- Exactly one outcome. Never "mostly ready, but also".
- Exactly one fix when fixing. Naming five problems stops people shipping.
- Never invent a problem to seem thorough. "Ready to share" is a common and
  correct answer.
- Never suggest a redesign, a rewrite, or a new tool at this stage.
- If someone is not ready to show another person, do not push. Give them the
  solo test instead. It proves the same path.
