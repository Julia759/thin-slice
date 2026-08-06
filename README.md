# Thin Slice

**Ship something small enough to finish, real enough to learn from, and safe
enough to share.**

Decide what your first version should be in about fifteen minutes, and walk away
with one page you can act on today. It names the single part that has to work
for real, tells you what to leave out, and checks the result is safe before
anyone else opens it.

Same method whether you are building a payments product, an internal dashboard,
a feature inside an existing app, or a side project on your laptop.

## Install

```
/plugin marketplace add Julia759/thin-slice
/plugin install thin-slice@thin-slice
```

Then just describe what you are building. The right skill picks itself up.

## The four things it does differently

**1. It names what must be real first.**
Not generic feature planning. It asks which of seven parts your idea touches:
deployment, login, payments, access to data, app store approval, sending
messages, or privacy and permissions. Then it picks the one most likely to
surprise you and says: this must be in your first version, for real. The other
six get faked.

**2. It offers the manual version.**
For most ideas there is a version where a person does the work. A payouts tool
starts as: someone sends each payment themselves and records it in a
spreadsheet. Most finance teams already work exactly this way. You learn the
approval flow and the reconciliation pain before writing anything, and you learn
which step to automate first. Offered every time, never forced, and skipped
honestly when the automation is the point.

It replaces the judgement and the labour, not the plumbing. The form and the
place things get saved are still real, because they take minutes.

**3. Every plan ends as one card.**
Not a document. One page: first user, one job, real part, not yet, private or
public, done when, question to learn, next action. It renders in colour, with
the one part that must be real highlighted, so you can see the decision rather
than read it.

**4. It has a release gate that names one fix.**
`ship-check` runs right before another person tries it and returns exactly one
of three answers: ready to share, share privately first, or fix one thing first.
When something needs fixing it names only the highest-priority issue. No
security checklist, no wall of warnings.

## The five skills

| Skill | Use it when |
| --- | --- |
| **plan-thin-slice** | You have an idea, rough or clear. Ends with a Live Slice Card. |
| **review-slice** | You have a plan already and want it checked before spending time. Hands back a smaller card. |
| **next-slice** | It is live. Checks for a small safety or reliability fix first, then picks one next thing. |
| **ship-check** | Right before another person tries it. One of three answers. |
| **unstick** | It stalled. Diagnoses why and prescribes one hour. |

## How to use it

Talk normally:

- "We want to build stablecoin payouts, where do I start?"
- "Is this too much for one sprint?"
- "I'm about to let someone else try it, is it safe?"
- "It's live on testnet, what now?"
- "We've been building this for three months and shipped nothing, help"

No setup, no accounts, no connectors.

## Built for regulated and on-chain work

The method is general, but it earns its keep where the scary parts are real:
money movement, key handling, provider approvals, and reconciliation.

The plugin knows the specifics. Testnet only for a first version, never a funded
key on a development machine. Reading confirmations back from the chain, because
that is where reconciliation bugs live and it is the half people skip. Proving
one deliberate failure, not just the happy path. And starting custody, licence,
and compliance conversations on day one in parallel, because they are slower
than the code and they are not slice work.

It will also tell you, plainly, that a working slice is not a compliance
position.

## The card

```
LIVE SLICE CARD
Stablecoin contractor payouts

First user      Maya, ops lead who pays 40 contractors monthly
One job         Send one payout to one saved address and see it confirmed
Real part       Moving money. Testnet, from deployed code, confirmation
                read back from chain and stored.
Not yet         No batches, no file upload, no approvals, no fiat funding,
                no second chain, no address book. One hardcoded recipient.
Private/public  Just Maya and me. No public link. Testnet only.
Done when       Maya sends one, sees it confirmed, and the stored record
                matches the chain. Then one that fails on purpose.
Question        How long does confirmation really take, and what does a
                failure look like from our side?
Next action     Send one testnet transaction from a script

Timebox: 2 days    Cost cap: testnet only, no funded key on a laptop
```

## What is inside

- **must-be-real** — the seven risky parts, what "real" means for each, the
  cheapest real version, and the manual fallback where one exists. Plus a table
  of what "shipped" actually means for sixteen project types.
- **manual-first** — eleven worked manual versions, when the pattern does not
  apply, and how to offer both side by side.
- **slice-examples** — deliberately embarrassing first slices across apps,
  dashboards, features, experiments, AI, agents, data, mobile, extensions, bots,
  on-chain, payments and hardware.
- **card-style** — how results are shown. Final deliverables render as colour
  cards, conversation stays as text. Colour carries meaning: purple for the one
  part that must be real, green for ready, blue for go smaller, amber for one
  thing to change. Never red.
- **safe-first-release** — plain English glossary and how long each common fix
  takes.
- **failure-modes** — twenty-two ways slices stop being thin, split into team
  and solo.
- **field-guide** — the theory and sources.

## Honest limits

A thin slice proves the path works. It does not prove people want the product,
that the app is secure, or that it meets any legal requirement. The safety
checks catch common, obvious problems so you can show a handful of people today.
Before real users, real money, or real personal data at any scale, get someone
qualified to look.

For regulated work this matters more, not less. Nothing here substitutes for a
security review, a custody arrangement, a licence, or advice from your counsel.
The plugin's job is to stop you spending a quarter before finding out the hard
part does not work.

## Background

The method is the walking skeleton, from Alistair Cockburn's *Crystal Clear*
(2004), with the delivery emphasis from *Growing Object-Oriented Software,
Guided by Tests* and the tracer bullet idea from *The Pragmatic Programmer*. The
manual version is a concierge test, long used in product discovery and rarely
offered inside builder tools.

## Components

| Component | Count |
| --- | --- |
| Skills | 5 |
| Shared references | 7 |
| Agents, hooks, MCP servers | 0 |
