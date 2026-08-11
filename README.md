# Thin Slice

**Ship something small enough to finish, real enough to learn from, and safe
enough to share.**

**Website:** [thin-slice-plugin.yuliiazol.chatgpt.site](https://thin-slice-plugin.yuliiazol.chatgpt.site)

In about fifteen minutes, Thin Slice helps you decide what to build first. You
leave with one page you can use today: the one part that needs to work for real,
what you can leave out, and what to check before someone else tries it.

Use it for a payments product, an internal dashboard, a feature in an existing
app, or the side project sitting on your laptop.

## Install in Codex

In a terminal, run:

```sh
codex plugin marketplace add Julia759/thin-slice
codex plugin add thin-slice@thin-slice
```

Start a new Codex task after installing so the five Thin Slice skills are
available.

## Install in Claude Code

```
/plugin marketplace add Julia759/thin-slice
/plugin install thin-slice@thin-slice
```

Then describe what you want to build. In either product, Thin Slice will guide
you to the right skill.

## What it does differently

### 1. Finds the part that needs to be real first

Thin Slice looks at the seven parts your idea depends on: deployment, login,
payments, data access, app-store approval, sending messages, and privacy and
permissions.

It picks the one most likely to cause trouble later and puts it in the first
version. The other parts can wait or use a temporary stand-in.

### 2. Suggests a manual first version

Many ideas can be tested before you automate everything.

A payouts tool could start with someone sending each payment manually and
tracking it in a spreadsheet. You learn how approvals and reconciliation
actually work before building a full payments system.

Thin Slice offers this option when it makes sense. It still keeps the basic flow
real: a form, a place to save information, and a way to complete the task.

### 3. Ends with one clear card

You get one page, not a long plan.

It includes:

- who will use it first;
- the one job they need to do;
- the part that must work for real;
- what is deliberately postponed;
- whether it should be private or public;
- what counts as done;
- what you are trying to learn; and
- the next action to take.

The key decision is highlighted so you can see it quickly.

### 4. Checks before you share

Run `ship-check` before another person tries the app.

It gives one answer:

- Ready to share
- Share privately first
- Fix one thing first

If something needs attention, it points to the one most important problem. You
get a clear next step rather than a long warning list.

## The skills

| Skill | Use it when |
| --- | --- |
| **plan-thin-slice** | You have an idea, whether it is rough or clear. You get a Live Slice Card. |
| **review-slice** | You already have a plan and want to make it smaller before you spend time building. |
| **next-slice** | Something is live and you need to decide what to improve next. |
| **ship-check** | Someone is about to try it and you want a quick final check. |
| **unstick** | The project has stalled and you need one useful action for the next hour. |

## How to use it

Talk normally:

- "We want to build stablecoin payouts. Where do we start?"
- "Is this too much for one sprint?"
- "I'm about to let someone try this. Is it safe to share?"
- "It's live on testnet. What should we do next?"
- "We've been building for three months and still haven't shipped. Help."

There is no setup, account, or connector required.

## For regulated and on-chain work

Thin Slice works for any kind of project. It is especially useful when the risky
parts involve money movement, keys, provider approval, or reconciliation.

For example, a first on-chain payment slice should:

- use testnet only;
- avoid funded keys on a development machine;
- read transaction confirmation back from the chain;
- store that confirmation; and
- include one intentional failure, not only a successful test.

It will also remind you to start custody, licensing, and compliance
conversations early. Those usually take longer than the code.

A working slice does not mean you are compliant.

## Example card

```
LIVE SLICE CARD
Stablecoin contractor payouts

First user      Maya, the operations lead who pays 40 contractors each month
One job         Send one payout to one saved address and see it confirmed
Real part       Moving money: testnet, deployed code, confirmation read from
                the chain and stored
Not yet         No batches, file upload, approvals, fiat funding, second chain,
                or address book. One hardcoded recipient.
Private/public  Maya and me only. No public link. Testnet only.
Done when       Maya sends one payment, sees it confirmed, and the saved record
                matches the chain. Then we test one failure on purpose.
Question        How long does confirmation take, and what does a failure look
                like from our side?
Next action     Send one testnet transaction from a script

Timebox: 2 days    Cost cap: testnet only; no funded key on a laptop
```

## A real run

[Expense tracker with my own categories](examples/expense-tracker.md) — one
afternoon, one person, from a three-part idea to a working tool reading a real
bank account. Includes the card, what the method got right, the two mistakes I
made in my first three saves, and the four bugs the run found in this plugin.

## What is included

- **must-be-real**: the risky parts to look for, what "real" means for each, the
  cheapest real version, and a manual option where one exists.
- **manual-first**: eleven examples of manual first versions, when they work, and
  when they do not.
- **slice-examples**: deliberately tiny first versions for apps, dashboards,
  features, experiments, AI tools, mobile apps, extensions, bots, payments,
  on-chain products, and hardware.
- **card-style**: guidance for showing results as simple colour cards. Purple
  marks the part that must be real; green means ready; blue means make it
  smaller; amber means change one thing. Red is not used.
- **safe-first-release**: plain-English explanations of common safety checks and
  the likely effort for each.
- **failure-modes**: twenty-two ways a slice can become too large, split between
  team and solo projects.
- **field-guide**: the method, background, and sources.

## What it cannot do

A thin slice can prove that the path works. It cannot prove that people want the
product, that the app is secure, or that it meets legal requirements.

The safety checks are meant to catch common problems before you show a small
group of people. Before handling real users, real money, or personal data at
scale, ask a qualified person to review the work.

For regulated products, this does not replace a security review, custody
arrangement, licence, or legal advice. The goal is simpler: find the difficult
part before you spend a whole quarter building around it.

## Background

The method draws on the walking skeleton idea from Alistair Cockburn's *Crystal
Clear* (2004), the delivery approach in *Growing Object-Oriented Software,
Guided by Tests*, and the tracer bullet idea in *The Pragmatic Programmer*.

The manual approach is a concierge test: doing the work by hand first to learn
what should be automated later.

## Components

| Component | Count |
| --- | --- |
| Skills | 5 |
| Shared references | 8 |
| Agents, hooks, MCP servers | 0 |
