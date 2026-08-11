# A real run: getting my own bank data into my own categories

*A walking-skeleton case study: finding the function everything else depends on and proving it first.*

## I thought I was building a dashboard

The original idea was:

> A dashboard to track my expenses, show how much money I have, and plan trips on a calendar.

That sounded like one product. It was really three.

I started thinking about charts, categories, screens, and how the trip calendar might work. Then I reached a question I had barely considered:

> Could my code read data from my N26 account at all?

Every other feature depended on the answer.

So I reduced the entire idea to one concrete job:

> Retrieve one real bank transaction and save it under a category I define myself.

Charts, trip calendar and polished interface are fluff in this case.

Only one thin path through the system, from my bank account to my own code.

## Banking data is surprisingly gatekept

I knew banks had APIs. I had not understood how difficult those APIs could be to access.

N26 provides account information through its PSD2 interface, but direct access is designed for regulated third-party providers and [requires a production QWAC certificate](https://support.n26.com/en-eu/security/open-banking-psd2/psd2-open-banking-for-third-party-providers).

Having an N26 account and access to my data as a customer did not give my code access to that data. A direct integration was impractical for a personal prototype.

I chose **Enable Banking** as an intermediary. It handles the regulated bank connection while my application handles authentication, transactions, and categorization.

Enable Banking also offers a [restricted production mode](https://enablebanking.com/docs/api/linked-accounts/) that lets an individual connect only their own whitelisted accounts. That was exactly the boundary I needed.

This was the first real learning from the project: the main function was not displaying expenses. It was getting the expenses in the first place.

## Proving the connection with fake data

I started in the sandbox.

I registered an application, generated an RSA private key and public certificate, configured JWT authentication, and tested the connection from a small Python command-line tool.

The first successful response was deliberately unexciting:

```text
Connected.
environment  SANDBOX
active       True
```

N26 was missing from Enable Banking’s sandbox list, so I couln't simulate it there. I used Nordea’s Finnish sandbox instead.

The authorization flow redirected me to a page that looked broken: the browser landed on Example Domain. But the address contained an authorization code. My script exchanged it for a session, found three simulated accounts, and confirmed that 38 transactions were available.

Then it printed one transaction.

That proved the complete technical path worked:

```text
private key → signed request → bank authorization → session → account → transaction
```

I still had no idea whether the same path would work with my real N26 account, but I had tested every step around that final uncertainty.

## Moving from simulation to my real N26 account

Sandbox and production applications are separate, so I registered a second application for production and generated a new private key.

I linked my N26 accounts, which activated the application in restricted mode. Linking only whitelisted the accounts; the script still had to run the authorization flow again to create an API session.

The next check returned:

```text
Connected.
environment  PRODUCTION
active       True
```

After N26 authorization, the script opened a session with three accounts and retrieved my real transactions.

That was the actual milestone.

The project still had no dashboard. It could now do the one thing every possible version of the product required: securely retrieve data from my own bank account.

## Real use uncovered a second problem

Once the bank connection worked, I used the tool on my actual expenses.

I tried to save a museum visit under one of my categories, but accidentally filed it under **groceries**.

Then I tried to correct it by running the save command again with **Fun**. The tool saved a different transaction instead: a bank transfer with no useful merchant name.

Two product problems appeared:

1. Saving an expense was different from recategorizing one.
2. A number shown in a temporary list could not safely identify a transaction later.

The tool needed a way to inspect saved entries, remove the wrong one, and file the intended transaction again.

I added commands to:

- list transactions;
- save a transaction under a custom category;
- show saved expenses and category totals;
- assign stable numbers to saved entries;
- remove an incorrectly saved entry.

I deleted both mistakes, found the museum transaction again, and saved it under **Fun**.

Changing your mind about a category turned out to be normal behaviour, not an edge case like Claude said lol. That learning only became available after the more fundamental API risk was resolved.

## What exists now

The project is still a command-line prototype, but it completes a real end-to-end job:

- authenticate with Enable Banking using signed JWTs;
- work with sandbox or restricted production access;
- connect to an authorized bank account;
- retrieve real transactions;
- list transactions without storing credentials;
- save selected expenses locally;
- group them into categories defined by the user;
- display category totals;
- remove and recategorize mistakes.

The user decides what the categories mean. 
Still deliberately unfinished

Several important limitations remain:

Bank consent expires, and I have not tested the complete reauthorization experience.

Transfers can still appear alongside expenses and need better filtering.

The script automatically uses the first authorized account instead of offering account selection.

Transaction matching and duplicate prevention need stronger rules.

The private-key and session setup is still too technical for a normal user.

There is no dashboard yet.

These next steps came from using the working path. I did not have to invent them in advance.

## What I learned

I began with a dashboard in mind. The most important work happened before there was anything to display.

Charts, categories, and trip planning all assumed that the bank connection would work. I had treated that assumption as an implementation detail, then discovered a regulated and surprisingly complicated access layer underneath it.

The rough command-line version was enough to cross every boundary that mattered: authentication, bank consent, account access, transaction retrieval, local categorization, and correction.

The question I should have started with was:

What has to be true for any of the rest of this product to work?

For this project, the answer was simple to ask and unexpectedly difficult to prove:

Can my code retrieve one real transaction from my own bank account?
