# Safe First Release

Plain English reference for the safety, reliability, and learning checks. Load
when someone needs a term explained, or when a fix needs to be described
concretely.

Written for people who are building something real but are not engineers. Every
term gets one line, no lecture.

## Small glossary

**Secret key** (also API key, token, credential). A long password that lets your
app use another service, like a payment tool or an AI model. Anyone who finds it
can use it, sometimes spending your money. It should never sit in the code
itself.

**Environment variable / hosting settings.** The place your hosting service
keeps secret keys, separate from the code. You paste the key in there once, and
the app reads it when it runs. Every hosting service has this, usually under
Settings.

**Test mode / sandbox.** A switch most payment tools have that runs the entire
flow with fake card numbers. Nothing is charged, nothing is real. Use it for
first releases, always.

**Fictional data / test data.** Made-up names and details belonging to no real
person. Obviously fake is better than realistic. "Test Customer One" is safer
than a name that could be somebody's.

**Log.** A running list of what the app did, kept by the hosting service. When
something goes wrong, the log tells you where. Adding one line that records "the
save worked" or "the save failed" costs almost nothing and saves hours.

**Access control.** Deciding who can open the thing. At this stage it does not
need to be sophisticated. A password on the page is real access control.

**Unlisted.** Reachable only by people who have the exact address, not findable
by searching. Good enough for showing a handful of people.

**Private browser window / incognito.** A browser window that forgets you. Use
it to see the app the way a stranger would, without your saved logins making
things work that would not work for them.

## The five plan questions, and why each exists

Asked in `plan-thin-slice`.

**1. What data is real and what can be fictional?**
Most first releases need no real data at all. Fake data cannot leak, cannot
embarrass anyone, and works just as well for proving the path.

**2. Who should be able to reach the live version?**
Most first releases should reach one to five named people. Deciding this on
purpose is different from leaving it open by accident, which is what usually
happens.

**3. What is the one main action?**
The single thing that must work. Naming it stops the test from becoming a
general poke around, which teaches nothing.

**4. How will you know it succeeded or failed?**
An app that fails silently wastes the test. The person tries it, something goes
wrong, they say "nice" politely, and you learn nothing.

**5. What question should this release answer?**
Written before building, this is what makes a disappointing result useful
instead of demoralising.

## Common fixes, and how long they actually take

Use these when recommending the smallest safe change. All are minutes, not
hours.

| Problem | The fix | Roughly |
| --- | --- | --- |
| Secret key sitting in the code | Move it to the hosting settings, then create a new key and delete the old one | 15 minutes |
| Real customer names or emails in the test data | Replace with made-up ones of the same shape | 15 minutes |
| Anyone with the address can open it | Add one shared password to the page | 20 minutes |
| Findable by search when it should not be | Mark it unlisted, or remove the public address | 10 minutes |
| No idea whether the main action worked | Add one line that records success or failure | 10 minutes |
| Real money could move | Switch the payment tool to test mode | 5 minutes |
| Unknown running costs | Set a spending limit in the provider dashboard | 10 minutes |
| Never tested as an outsider | Open it in a private window on another device, do the main action | 10 minutes |

If a problem genuinely cannot be fixed in this size, say so plainly rather than
pretending. Some things are real work and deserve to be named as such.

## Limits, stated honestly

These checks catch common, obvious problems. They are worth doing and they are
not the same as:

- **A security review.** That looks for ways someone could deliberately break
  in. This does not.
- **A privacy assessment.** That covers what you are allowed to collect, how
  long you may keep it, and what you must tell people. This does not.
- **Legal compliance.** Rules differ by country and by industry, and they apply
  to real users, not to a test with three friends.
- **Evidence that people want the product.** A thin slice proves the path works.
  Whether anyone wants it is a separate question and a separate kind of test.

The honest position: these checks make it safe enough to show a handful of
people today. Before real users, real money, or real personal data at any scale,
someone qualified should look at it.

## Tone guidance

People reaching these checks have usually done something hard and are nervous
about the last step. Be practical and warm about it.

- Lead with what is fine, then name the one thing to fix
- Never list five problems at once. One, fixed, then re-check
- "Ready to share" is a common and correct answer. Do not invent problems to
  look thorough
- Do not use fear. Describe the specific consequence in one line, then the fix
- Never suggest a rewrite or a new tool at this stage
