# Slice Examples

Calibration material. Load when a draft slice needs shrinking, or when someone
cannot picture how small "small" is.

Every example is deliberately embarrassing. That is the correct size. If the
slice would be comfortable to demo, it was too big.

Format: the slice, what is hardcoded, what it proves.

For the manual version of an idea, see `manual-first.md`. Offer both.

## Quick pairs

When someone needs to see the choice quickly:

| Idea | Manual version (hours) | Built slice (days) |
| --- | --- | --- |
| Tracker app | A shared spreadsheet | One form, one saved record, one list view |
| Dashboard | You pull the numbers weekly and email them | One real number, real source, deployed page |
| AI writing tool | They send input, you run it and reply | One input, one real model call, cost logged |
| Feedback summariser | You read it and write the summary | One real model call over saved feedback |
| Job matcher | You find three roles by hand | One search against the real data source |
| Booking | Form plus your own calendar and email | Form writes to a real calendar, real confirmation |
| Marketplace | You introduce both sides yourself | One listing, one enquiry, one real notification |
| Alerts | You check daily and message people | One scheduled job, one real alert |

In every row the manual version replaces the judgement, not the storage. If the
built version needs a database, so does the manual one, and it takes the same
ten minutes either way.

## New app or service

**Slice.** A public URL returns one page with one number read from a real
database row inserted by hand.
**Hardcoded.** Everything else. No routes, no styling, no accounts.
**Proves.** Deploy path works, and deployed code can reach the database.

**Next slice.** A visitor pastes text in one box, presses one button, sees one
transformed result. No account, no history, no saving.

## Dashboard

**Slice.** One deployed page shows one real number, pulled from the real data
source, refreshed by the real scheduler.
**Hardcoded.** The metric, the date range, the filters, the layout.
**Proves.** Access to the data source from production, credentials, and the
refresh mechanism. Those three are what actually break. Charts are easy.

**Common mistake.** Building six charts against a local CSV export. That proves
nothing, because the export is the part that will not work in production.

## Feature inside an existing product

**Slice.** The feature is merged, deployed, and switched on behind a flag for
exactly one internal account. It does the smallest version of its job, once.
**Hardcoded.** Every option, every edge case, every permission variant.
**Proves.** The feature survives the real codebase, the real deploy, and the
real data. Integration with existing code is the risk, not the feature logic.

**Do not.** Build it fully on a branch and merge at the end. That is a cutover,
and cutovers are where features die.

## Experiment or A/B test

**Slice.** The experiment is live in production, splitting real traffic, with
both variants doing almost nothing different, and one metric recording.
**Hardcoded.** The variant content, the audience, the split.
**Proves.** Assignment works, tracking fires, and the metric lands where you can
read it. Run this before the real variants exist.

**Why it matters.** Broken tracking discovered after two weeks of traffic wastes
the whole experiment. Prove the plumbing with a null test first.

## Service extracted from a monolith

**Slice.** One named endpoint, for one narrow use case, runs in the new service
in production and serves real traffic. Everything else still hits the old path.
**Proves.** The new service can carry real load and real data.
**Then.** Move one use case per slice. The old code is deleted only once nothing
uses it. There is never a cutover.

## AI or LLM feature

**Slice.** One input calls the real provider from deployed server code, returns
one answer to the surface, and logs token count and latency.
**Hardcoded.** Prompt, model, parameters.
**Proves.** Keys work in production, latency is survivable, cost is visible.
**Before the first call.** Set a hard spend cap in the provider dashboard.

**Not proved.** Answer quality. That is a later slice with an evaluation set.

## Agent or tool-calling system

**Slice.** The agent calls exactly one real tool, once, for one hardcoded task.
Both the tool result and the final answer are visible.
**Skipped.** Memory, planning, retries, multi-step loops.
**Proves.** The tool contract and the permission model. The loop is the easy
part.

## Data pipeline

**Slice.** A scheduled job runs in the cloud, fetches one source, writes one row,
and the rows visibly accumulate day over day.
**Hardcoded.** Source, schedule, fields.
**Proves.** Scheduling in production, which is where these stall. Local scripts
prove nothing.

## Mobile app

**Slice.** Installs on a real device through TestFlight or an internal track,
shows one screen, calls the deployed backend once.
**Proves.** Signing, store tooling, and the device-to-server path. Signing is
the monster. Meet it in hour one, not week six.

## Browser extension

**Slice.** Loads on one hardcoded site, changes one word, installable by one
other person.
**Proves.** Manifest, permissions, and the install path.

## Bot

**Slice.** Online, responds to one command with one hardcoded string, triggered
by someone else.
**Proves.** Hosting, token handling, and the platform's approval quirks.

## On-chain app

**Slice.** A page connects a wallet, sends one hardcoded testnet transaction,
and displays the confirmed hash read back from the chain.
**Proves.** Wallet connection, signing, RPC, and reading state back. Those four
consume the first weekend.
**Never.** Mainnet, or a funded key on a development machine.

## Smart contract

**Slice.** One contract, one function, deployed to testnet, called once from a
script, state readable in a block explorer.
**Proves.** Toolchain, deploy path, verification.

## CLI tool

**Slice.** Published to the package registry, installable by a stranger with one
command, prints one line.
**Proves.** Packaging and distribution, the part people postpone forever.

## Payments or money movement

**Slice.** One test account moves the smallest amount to one hardcoded
destination, the reference is stored, and a status webhook updates the record.
**Skipped.** Balances, fees, retries, multiple currencies, any UI.
**Proves.** Key handling, settlement timing, webhook reliability, and whichever
approval your provider requires.

## Stablecoin payouts

**Slice.** One payout, to one saved address, on testnet, sent from deployed
code. The confirmation is read back from the chain and stored against the
record.
**Hardcoded.** The recipient, the amount, the asset, the network.
**Skipped.** Batches, file upload, approvals, fiat funding, multiple chains,
address book, retries, any UI beyond a button.
**Proves.** Key handling, how long confirmation really takes, and whether your
record matches the chain afterwards. Reading the confirmation back is the half
people skip and where reconciliation bugs live.
**Then prove one failure.** Send one that will not go through and watch what
your system does. Most first versions only handle the happy path.
**Never.** Mainnet, or a funded key on a development machine.

## Payment reconciliation

**Slice.** One incoming payment is matched to one invoice automatically, and the
match is visible with the reason it matched.
**Hardcoded.** The matching rule, the date range, the currency.
**Proves.** That you can read both sides from their real sources and line them
up. The matching logic is easy. Getting both sides is not.

## Enterprise integration

**Slice.** One record created in the new system appears correctly in the legacy
system of record, through the real middleware, with audit logging on, confirmed
by one person from the operations team role-playing the real process in
production.
**Proves.** The middleware contract, the audit requirement, and the working
relationship with the team that owns the legacy system. The relationship is part
of the deliverable.

## Hardware or device

**Slice.** One device sends one reading to a deployed endpoint, visible from a
phone somewhere else.
**Proves.** The network path, which never works the first time.

## The pattern underneath all of them

One action. One person. Real conditions. Everything else faked, hardcoded, or
postponed.
