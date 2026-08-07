# A real run: expense tracker with my own categories

One afternoon, one person, one project. This is what the method actually did,
including the parts that went wrong.

---

## The idea, as I first said it

> A dashboard to track personal expenses, and a calendar view where I can log
> trips I want to do, and I want to pull my banking app data, and see how much
> money I currently have.

Three projects in one sentence. The first thing the method did was refuse it.

## What it asked

Not "what features do you want". These:

- What does this do, for one person, in one sentence, with no "and" in it?
- Which of the seven risky parts does it touch?
- Where does the data come from?
- What would you need to see to call it working?
- What do you actually want to find out?
- Will anyone else ever open it?

Six questions, a few minutes. I answered them myself. That mattered later.

## The card it produced

```
LIVE SLICE CARD
My expenses, in my own categories

First user      Me. Only me for now.
One job         See my expenses grouped into categories I define myself
Real part       Bank data access. One real transaction, fetched by
                deployed code, stored. Sandbox first, then my own account.
Not yet         No trip calendar. No balance view. No charts, history,
                budgets, rules, or auto-categorising. No login.
Private/public  Just me. Unlisted address, password on the page.
Done when       One real transaction from my bank sits in one category
                I made up, and it is still there when I reopen.
Question        Can I get read access to my own N26 account at all,
                without a company or a licence?
Next action     Sign up at the provider, pull one sandbox transaction
                from a script. Before any interface.

Timebox: one sitting, then waiting on approval
```

The trip calendar and the balance view, the two things I had been most excited
about, both went under "not yet". They are still not built. I have not missed
them.

## What actually happened

**The research changed the plan before any code.** Checking whether my bank had
an API turned up two things. My bank's own interface needs a licence a private
person cannot get. And the free provider everyone recommends in blog posts had
closed to new signups. Both facts were less than five minutes of looking, and
both would have been discovered a week in.

**The scary part came first.** Not the dashboard, not the categories. Signing up
with a provider, generating keys, registering an application, connecting an
account. All the tedious approval work, at the very start, when I still had
energy for it.

**The practice run came before the real one.** A test bank with fake Finnish
data proved the code worked. Only then did I do the second registration for real
money. When the real one failed I knew it was my account setup, not my code,
because the code had already worked once.

**Then it printed one real transaction.** Question answered: yes, a private
person can read their own bank data. That was the whole point of the first
slice, and it was answered before a single screen existed.

## What it cost

An afternoon. No dashboard, no calendar, no charts.

What I have instead is the certainty that the hard part works, and a tool I
actually used the same day.

## What went wrong

The honest part, since a case study where everything works is not worth reading.

**I chose the wrong category twice in my first three saves.** Filed a museum
under groceries, and accidentally filed a bank transfer as an expense. There was
no way to undo either.

That turned out to be the most useful thing that happened. Picking a category is
the main action of this whole tool. If getting it wrong is permanent, the file
becomes junk within a week and you stop trusting it. So the next slice was not a
chart or a calendar. It was being able to fix a mistake.

I would not have found that by planning. I found it by using the thing on my own
money on the same day I built it.

**Still unfinished, deliberately:** the bank connection expires and I have not
yet tested what the tool does when it does. Transfers can still be filed as
expenses, which is wrong. Both are on the list. Neither blocks using it.

## What the run changed about this plugin

Using it on something real found four bugs in the method itself. All four are
fixed in the current version.

1. **It assumed instead of asking.** It guessed I had never deployed anything,
   from context. Now the rule is explicit: ask, never infer, because guessing low
   is patronising and guessing high produces a card nobody can act on.
2. **It offered me a menu of jobs it had invented**, I picked one, and that
   laundered its assumption into my choice. Now the one job comes from the
   person's own words, and listing back only what they actually said is treated
   as different from inventing options.
3. **It filled in card fields nobody had said out loud.** Done when, question,
   first user. Now every value is checked against something the person actually
   said, with those four named as the ones most commonly invented.
4. **It did not ask what had changed between sessions.** I connected my bank
   account without mentioning it, because to me it had already happened. Now
   every skill that runs after building starts asks what changed first.

## The honest limits

This proved the path works. It did not prove anyone else wants this, that it is
secure, or that it would survive more than one user.

It is a private tool for one person, holding one person's data, on one laptop.
That was the point.
