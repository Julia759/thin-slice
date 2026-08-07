# What Must Be Real First

The seven parts that surprise people. Reference for the central decision in
`plan-thin-slice` and the main check in `review-slice`.

## Why this list exists

Faking is cheap in the wrong places and expensive in the right ones. Skipping a
feature costs nothing. Skipping the part you do not control postpones the only
thing you needed to find out.

These seven parts share three traits. They are outside your control, they fail in
ways you cannot predict from reading about them, and everything else ends up
depending on them. So exactly one of them, whichever is riskiest here, must be
real in the first slice. The rest can be faked.

## The seven

For each: why it surprises, what "real" means in slice one, the cheapest real
version, and the manual version that tests the same thing without building.

### 1. Deployment

**Why it surprises.** Working on a laptop teaches you nothing about the machine
it will actually run on. Missing settings, secrets that are not there,
permissions, the build behaving differently. Always slower than expected, and
completely invisible until attempted.

**Real means.** Running somewhere another person can reach, put there by a
command or a push rather than by hand.

**Cheapest real version.** One page that says "hello", deployed to any free
host, with nothing else in it.

**Manual version.** None. This one cannot be faked. If it is your riskiest part,
it must be built, and it should be the first hour of work.

### 2. Login and accounts

**Why it surprises.** Password resets, expiring sessions, the difference between
signing in and staying signed in, and one person seeing another person's data.
That last one is the failure people discover in front of a user.

**Real means.** Two different accounts, on two different devices, each seeing
only their own data.

**Cheapest real version.** Use a hosted sign-in service rather than building it.
Two test accounts is enough.

**Manual version.** Send each person their own private link with a code in it.
No accounts, no passwords. Tests whether people will come back, which is usually
the real question.

### 3. Payments and moving money

**Why it surprises.** Approval to handle money takes days or weeks. Then there
are refunds, failed cards, currency, tax, and the gap between "payment started"
and "money actually arrived". That gap is where most of the surprises live.

**Real means.** One payment completes in test mode, and you can see the record
on your side. Test mode is a switch almost every payment tool has that runs the
whole flow with fake cards and no real money.

**Cheapest real version.** A payment link from a hosted provider. No checkout to
build.

**Manual version.** Send an invoice by email and take a bank transfer. If people
will not pay by transfer, they will not pay by card either. This tests
willingness to pay, which is the part that actually matters.

**If money moves on chain**, the same rule applies with sharper edges:

- **Testnet only.** Never mainnet for a first version, and never a funded key on
  a development machine. If the slice cannot be proven on a testnet, that itself
  is worth knowing on day one.
- **What is actually risky** is rarely the transfer call. It is key handling,
  how long confirmation really takes, what a failed or stuck transaction looks
  like from your side, and whether your record matches the chain afterwards.
- **Real means** one transaction submitted from deployed code, confirmed, and
  the confirmation read back and stored. Reading it back is the half people
  skip, and it is where the reconciliation bugs live.
- **Prove one failure too.** Send one transaction that will not go through and
  watch what your system does. Most first versions handle only the happy path
  and discover the rest in front of a user.
- **Custody, compliance, and licence questions are not slice work.** They are
  real, they are slower than the code, and they need qualified people. Start
  them in parallel on day one rather than treating them as a later step.
- **Manual version.** Someone sends the payment themselves from the company
  wallet and records it in a spreadsheet. This is what most teams already do,
  and it tests demand, the approval flow, and the reconciliation pain without
  writing anything.

### 4. Access to data you do not own

**Why it surprises.** Someone else's system behaves differently from production
than from your laptop. Credentials, network rules, rate limits, and a shape that
turns out not to match what you assumed.

Applies to company warehouses, third-party services, model providers, chains,
and any system somebody else controls.

**This is not about your own storage.** Saving what your own app creates is not
on this list. See "what not to fake" below. The risky one is reaching into
something you do not control.

**Real means.** One real record, fetched by deployed code, from the real source.
Not an export, not a copy, not a sample file.

**Cheapest real version.** One number on one page, pulled live.

**Manual version.** Pull the data by hand once and paste it in. Tests whether
anyone wants the answer before you build the pipe to get it.

### 5. App store or distribution approval

**Why it surprises.** Signing, certificates, review queues, and rejections for
reasons unrelated to your app. Days to weeks, entirely outside your control, and
it blocks everything behind it.

**Real means.** An empty app installs on a real device through the real channel:
TestFlight, an internal track, or a store listing.

**Cheapest real version.** One blank screen, submitted and installed. Do this in
week one, before the app exists.

**Manual version.** Build it as a web page first. Same journey, no store, no
review. Many apps never need to be apps.

### 6. Sending emails or messages

**Why it surprises.** Sending is easy. Arriving is not. First messages from a
new sender land in spam routinely, and you will not know unless you check
somebody else's inbox.

**Real means.** One message arrives in someone else's inbox, from the address
you intend to use, not in their spam folder.

**Cheapest real version.** Send one real message to one friend and ask where it
landed.

**Manual version.** Send it yourself from your normal email account. Tests
whether the message is worth receiving before you set up sending infrastructure.

### 7. Privacy and permissions

**Why it surprises.** Being open to more people than you meant. One person
seeing another's information. Storing something you should not have kept. These
surface in front of a real user, which is the worst place.

**Real means.** You can state exactly who can reach it, and you have checked
that this is actually true, not just intended.

**Cheapest real version.** One shared password on the page, or an unlisted
address. Then open it in a private browser window on another device to confirm.

**Manual version.** Keep the data in a spreadsheet only you can open, and handle
requests yourself. No system, no exposure.

## What not to fake

Faking is for **work and features**, not for plumbing. Some things are now so
cheap to do properly that faking them costs more effort than building them, and
produces a worse test.

**Build these normally, from the first version:**

| Thing | Why build it | Roughly |
| --- | --- | --- |
| A database for what your own app creates | A hosted one takes minutes and never has to be replaced later. Data that vanishes on refresh makes the test meaningless. | 10 minutes |
| Sign-in, if it is genuinely needed | Use a hosted sign-in service. Building your own is the mistake, using one is not. | 30 minutes |
| Taking a payment, if the whole point is charging | A hosted payment link, in test mode. No checkout to build. | 20 minutes |
| Sending one email | A hosted sending service, or your own email client for the very first version. | 15 minutes |
| Somewhere to deploy | Free tier, connected to the repo. | 20 minutes |

**Fake these instead:**

- The work a person would do: writing the summary, picking the matches, checking
  the result. That is where the real learning is.
- Everything around the one job: settings, filters, search, exports, admin
  screens, second user types.
- Systems you do not control yet, and anything needing someone else's approval.
- Volume. One record, one user, one case.

**The test.** If it takes ten minutes with a hosted service and the app is
pointless without it, build it. If it takes a week, or if a person could do it
by hand while you learn whether anyone cares, fake it.

A common error is faking storage and building features. That produces a demo
that impresses nobody and teaches nothing, because the moment anyone refreshes
the page their work is gone.

## Picking the one

Ask which of the seven applies at all. Usually two or three do.

Then pick the single one that is **most outside your control and hardest to
undo later**. Rough order when several apply:

1. App store or distribution approval, if any: slowest, and entirely outside
   your control
2. Payments, if money is involved: approval times plus real consequences
3. Deployment: nothing else can be tested until this works
4. Access to data: usually the real technical unknown
5. Privacy and permissions: cheap to get right early, expensive to fix after
   people are in
6. Login and accounts: often postponable much longer than people think
7. Sending messages: important, but usually a small fix once discovered

If none of the seven applies, say so plainly. The riskiest part is then whatever
the person has personally never done before, and the first slice should include
that instead.

## What "shipped" means, by project type

The most common self-deception is calling something done while it is still
private.

| Building | Shipped means |
| --- | --- |
| Web app | A public URL loads on a machine that is not yours |
| Internal tool | A colleague opens it from their own machine |
| Dashboard | One real number, real source, deployed page, real refresh schedule |
| Feature in an existing product | Merged, deployed, switched on for at least one real account |
| Experiment | Running in production, splitting real traffic, one metric recording |
| API or service | A stranger with the address and a key gets a real response |
| Data pipeline | A scheduled run happens without you starting it, and a row lands |
| AI feature | A real call from deployed code, result reaches the surface, cost visible |
| Agent | One real tool call executes, result and answer both visible |
| Mobile app | Installs through the real distribution channel, not a cable |
| Browser extension | Someone else can install it |
| CLI tool | Someone else can install it with one command |
| Library or package | Published to the registry, and someone else adds it as a dependency and builds against it successfully |
| Bot | Someone else can trigger it and get a reply |
| Smart contract | On a public testnet, called once, state readable in an explorer |
| Game | Playable by someone else without a build step |
| Newsletter or email | A real email arrives in someone else's inbox |

Underneath all of them: **one person who is not you, in real conditions, without
you present to make it work.**

## The seven thinness checks

Used by `review-slice`. A slice passes only if all are true.

1. **End to end.** Crosses every layer from the surface a person touches down to
   storage and any outside system.
2. **Real path.** Uses the production route, not a shortcut that gets deleted.
3. **Live.** Reachable by someone who is not the builder.
4. **Automated release.** Deployed by a command or a push, not by hand.
5. **Thin.** Contains no genuinely useful feature.
6. **Real part included.** Contains the one thing from the seven that must be
   real here.
7. **Observable.** A human can tell whether it worked.

Failing 1, 3 or 6 means the slice de-risks nothing. Say that first.

## Estimation correction

First plans run three to five times bigger than needed, consistently, for
everyone. Correct upward, then cut scope until it fits the timebox.

Routinely mistaken for small: authentication, file upload, payments, anything
real-time, email deliverability, app store submission, "just a simple
dashboard", and anything needing someone else's approval.
