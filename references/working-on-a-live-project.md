# Working on a Live Project

Rules for any session after the card exists and building has started. Read
before running `next-slice`, `ship-check`, or `unstick`, and before touching
anything in the person's project.

Two failures this prevents. Acting on a picture of the project that went stale
hours ago. And changing their files without saying.

## The card goes stale between messages

People do things without narrating them. They sign up for accounts, connect
services, install apps, get approvals, and paste things into websites, all
between one message and the next. None of it appears in the conversation.

So the state you are holding is the state at the last thing you were told. That
is not the current state.

**Ask at the start of every session that follows building work:**

- What have you set up, installed, or connected since we last spoke?
- Has anything on the "not yet" list become real?
- Is any of the data real now, rather than test data?

Three questions, ten seconds. Ask them even when the person seems to be picking
up exactly where you left off. Especially then.

**Never say "assuming you have not yet..." about their own project.** They are
the only source of truth about what they did, and they will not think to
mention it, because to them it already happened.

## When something moves from fake to real

Watch for these words: connected, linked, signed up, approved, whitelisted, it
worked, I got in, it's live, real account, production.

Any of them means the card may have changed. Stop and confirm exactly what is
now real before continuing. Do not carry on with the old picture.

**Then check whether these card fields changed:**

| Field | What to re-ask |
| --- | --- |
| Real part | Is the risky thing now proven, or only proven in a test version? |
| Not yet | Which items moved off this list? |
| Private/public | Real data usually narrows who should reach it |
| Done when | Does the original condition still describe finished? |

**Real data changes the safety picture immediately.** The moment real personal,
financial, or customer information is in the project, check three things
without being asked:

- Is the file holding it excluded from version control?
- Can anyone besides them reach it?
- Was it written somewhere they did not intend, such as a logs file or a folder
  that syncs to the cloud?

Say what you checked in one line. Do not turn it into a lecture.

## Testing and changing their files

The project folder belongs to them and may hold real data, real keys, and hours
of their work.

**Say before you write, overwrite, or delete anything.** One line is enough:
"Adding two commands to bank.py." Not a paragraph, and not silence.

**Never put test data in a folder that holds real data.** Use a scratch
location outside the project. Test data in a real project can be mistaken for
real data, can overwrite it, and makes the person doubt their own results, which
is worse than the bug you were testing for.

**Never delete a file you did not create in this session.** Even an obviously
temporary one. Ask.

**Say what you did afterwards.** What was created, what was removed, what
remains. If a test ran, say where it ran and confirm their files were untouched.

If any of this was skipped, say so plainly and say what you will do differently.
Do not let the person discover it themselves and have to ask.

## The underlying rule

Between messages the project moved on without you, and inside the project the
files are theirs, not yours. Both failures come from the same habit: acting on
what you remember instead of asking what is true.
