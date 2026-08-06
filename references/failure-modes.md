# Failure Modes

Why thin slices stop being thin, or stop happening at all. Used by
`review-slice` and `unstick`.

Split into two sets, because teams and solo builders fail differently.

---

# Team and product failure modes

## Horizontal milestones

**Symptom.** Milestone one is the data layer. Milestone two is the API.
Milestone three is the UI.
**Why it breaks.** Nothing integrates until the end, so all integration risk
survives, just later and costlier.
**Fix.** Rewrite milestone one as one actor completing one action across all
three layers.

## Routing around the monster

**Symptom.** The slice covers the new components and stubs the legacy system,
the provider, the chain, or the compliance step.
**Why it breaks.** The slice proves the team can build easy things.
**Fix.** Invert the stubbing. Make the scary component real, fake the rest.

## Prototype in disguise

**Symptom.** The code will be deleted afterwards, or is written in a throwaway
stack.
**Why it breaks.** Prototypes teach feasibility. Slices teach you about your
actual production environment and become the foundation.
**Fix.** Commit to keeping it, or call it a spike and stop expecting the
benefits.

## Stops at staging

**Symptom.** Works in a test environment. Production deploy is a later ticket.
**Why it breaks.** Most unknown work is in the last mile: approvals, secrets,
networking, security review, DNS, monitoring access. Deferring it means meeting
it under launch pressure.
**Fix.** Go live with no useful functionality. Hide it behind basic auth, a
private subnet, or no public DNS. Internal users must still reach it.

## Manual release

**Symptom.** A person copies artifacts or clicks through a console.
**Why it breaks.** Without automation there is no feedback loop, and pipeline
work gets deferred until feature pressure makes it impossible.
**Fix.** A crude pipeline counts. Written-down manual steps are acceptable. Zero
pipeline is not.

## Gold-plated layer

**Symptom.** One layer is polished while others are missing.
**Fix.** Cut the finished layer back to match the thinnest one.

## Useful functionality in slice one

**Symptom.** The first release does something a user would want.
**Why it matters.** Not fatal, but the feedback arrived later than it could
have.
**Fix.** Apply the reduction test twice.

## No observability

**Symptom.** It runs, nothing logs, nobody can prove it worked.
**Fix.** One log line and one metric in the real tooling.

## Missing the people layer

**Symptom.** Every technical integration is proven, no human one is.
**Why it breaks.** Process and approvals are the slowest integrations in any
organization.
**Fix.** Role-play one real use case in production with the real people.

## Coordination theatre

**Symptom.** Teams agree on a diagram, build separately, assume the pieces will
meet.
**Why it breaks.** Diagrams hide differences in assumptions. Differences appear
only when components actually connect.
**Fix.** Connect them in week one, even with fake payloads.

## Slice one ships, then nothing does

**Symptom.** The team pauses shipping for weeks to build things properly.
**Why it breaks.** The benefit compounds only if the system keeps running while
it grows.
**Fix.** Every slice ships. Refactoring rides inside slices.

---

# Solo and side project failure modes

## Localhost forever

**Symptom.** Months of work, runs beautifully on one machine, "I'll deploy when
it's ready."
**Why.** Deploying gets saved for later, so the project has no external
existence, so skipping a weekend costs nothing.
**Exit.** Deploy it broken, today.

## Scope creep at midnight

**Symptom.** The idea was one thing. It now has three subsystems and works on
none of them.
**Why.** Adding is fun and requires no decisions. Finishing requires calling
something good enough.
**Exit.** Put the original one sentence at the top of the README. Park
everything outside it.

## Stack shopping

**Symptom.** Four empty repos, strong framework opinions, no running code.
**Why.** Comparison feels productive and risks nothing.
**Exit.** Use whatever was used most recently. Familiar beats correct.

## Tutorial loop

**Symptom.** Fifth course on the same topic, nothing built outside lessons.
**Why.** Tutorials give steady feedback. Building gives silence and errors.
**Exit.** Rebuild the current tutorial's project from scratch without the video.
One hour. It will be bad.

## Foundations first

**Symptom.** Auth, schema, folder architecture, design tokens, admin panel. The
actual idea has never run.
**Why.** Those parts are well documented and feel professional. Nobody abandons
a project for lack of them.
**Exit.** Hardcode a user, hardcode the data, make the core action work today.

## Met the monster too late

**Symptom.** Good progress, then a hard integration, then silence.
**Exit.** Extract the blocked part into one isolated file with no project around
it. Make just that work.

## Rewrite spiral

**Symptom.** Third start. Each version cleaner, none finished.
**Why.** A fresh repo removes the discomfort of imperfect old code and restores
the pleasant early phase.
**Exit.** No rewrite. Deploy what exists, then change one thing.

## Perfectionism before contact

**Symptom.** Endless polish on something nobody has used.
**Exit.** Send it to exactly one person. Not a launch.

## Waiting for a block of time

**Symptom.** "When I have a free weekend." The weekend goes elsewhere.
**Why.** The project is not broken into pieces that fit an hour.
**Exit.** Define a one-hour slice. If none exists, the slices are too big.

## Silent cost anxiety

**Symptom.** Avoiding the project for no stated reason, usually one touching
paid APIs.
**Exit.** Set a hard spend cap. Ten minutes, and the dread goes.

## Permanent fakes by accident

**Symptom.** The stub from slice one is still there a year later and nobody
decided that.
**Why it is subtle.** Keeping a good-enough external service can be correct. The
failure is the absence of a decision.
**Exit.** Keep a stub register: what is faked, what for, when it gets replaced,
whether keeping it is fine.

## Interest genuinely gone

**Symptom.** It works. There is no desire to touch it.
**Read.** The project already delivered what it was for. That is a finished
project, not a failed one.
**Exit.** Choose an ending on purpose: park it with a README, write up what was
learned, or hand it over. Drifting is the worst option.
