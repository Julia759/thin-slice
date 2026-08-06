# The Manual Version

For every idea there is usually a version that tests the same journey with no
software behind it. Offer it every time. Never force it.

## The principle

Software automates a journey. Before automating it, run the journey by hand.

The person on the other end often cannot tell the difference, and does not care.
They wanted the outcome, not the machinery. Meanwhile you learn whether they
want it at all, what they actually ask for, and where the journey really breaks,
all in a fraction of the time.

This has a name in product work: a concierge test. You are the product, for now.

## Worked examples

The pattern is always: same journey, same outcome for the user, no automation.

**Travel planner.** A form asks for one travel preference. You receive it and
email back one suggested itinerary you wrote yourself. No accounts, no
recommendation engine, no scoring. The form entries still get saved somewhere
real, because losing them would be silly.

**Job matching.** People send you their situation. You reply with three roles
you found by hand. You learn what people actually want before building
matching logic that guesses wrong.

**Meal planning.** One form, one week of meals written by you. You find out fast
whether people follow a plan at all, which is the real question.

**AI writing tool.** People send you the input. You run it through a chat window
yourself and send back the result. Tests whether the output is good enough to
want, before building any product around it.

**Marketplace.** You are the marketplace. Both sides message you, you match them,
you introduce them. Every marketplace should start this way. The hard part is
supply, not software.

**Payouts, including stablecoin payouts.** Someone on the team sends each
payment themselves and records it in a spreadsheet. Most finance teams already
work this way. It tests the approval flow, the reconciliation pain, and how
often recipients get their details wrong, which is what the product will
actually have to solve. Build once the spreadsheet genuinely hurts, and you will
know exactly which step to automate first.

**Payment reconciliation.** You match the incoming payments to invoices by hand
for two weeks. You learn the real matching rules, which nobody can describe
correctly in advance.

**Analytics dashboard.** Pull the numbers by hand once a week and send a short
email. You learn which numbers people actually open, and it is never all of
them.

**Alerts or monitoring.** Check it yourself once a day and message people when
something changes. You discover what actually deserves an alert.

**Booking system.** A form, then you confirm by email and keep a calendar
yourself. Tests demand and the awkward parts of scheduling before building
availability logic.

**Community product.** A group chat and a spreadsheet. Almost every community
product should start here and many should stay.

**Personalised recommendations.** You pick them by hand for the first twenty
people. This teaches you the rules a system would need, which you cannot guess
in advance.

**Internal approval tool.** A shared document and a message when something needs
approving. Tests whether the process works before encoding it, and processes
change more than people expect.

## Manual does not mean no software

The manual version replaces the **judgement and the work**, not the plumbing.

A form that collects requests is software. So is the place those requests are
stored. Both take minutes with hosted services and both should be real. What is
manual is the part in the middle: you reading the request and doing the thinking
a system would eventually do.

The failure to avoid is collecting requests into an inbox you forget to check,
or a page that loses everything on refresh. That is not a manual version, it is
a leak.

## When it does not apply

Say so plainly rather than forcing it. There is no manual version when:

- The point is the automation itself: speed, scale, or volume no human can match
- It is developer infrastructure, a library, or a tool for machines
- The riskiest part is deployment, distribution approval, or a technical
  integration, which is what the slice must prove
- Doing it by hand would mean touching data you should not see

When it does not apply, say one line about why and move to the built slice. Do
not stretch the idea to fit.

## How to offer it

Always present both, side by side, then let the person choose.

```
Two ways to test this journey:

Manual: [what you do by hand, and what the person receives]
  Time: [hours]
  Answers: whether people want this at all

Built:  [the thin slice with the real part]
  Time: [hours or days]
  Answers: whether it works technically

[One line on which fits their risk, and why.]
```

Rough guide for the recommendation:

- Nobody has confirmed they want this: start manual
- People clearly want it and the question is whether it can be built here: build
  the slice
- Both are unknown: manual first, because it is faster and the answer changes
  what you build

## Where it usually leads

The manual version is not a detour. It normally produces:

- The exact wording people use, which becomes the interface
- The steps that actually matter, which is rarely the full flow imagined
- Evidence about whether anyone wants it, before spending weeks
- A first user relationship, because someone helped by a person remembers it

Many manual versions run for months. That is a success, not a delay. Automate
the step that hurts most, when it starts hurting, and not before.

## The honest limit

A manual version tests demand and the shape of the journey. It does not test
whether the software can be built, whether it holds up under load, or whether
the integrations work. If those are the real questions, build the slice instead.
