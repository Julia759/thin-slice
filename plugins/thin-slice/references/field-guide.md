# Field Guide

Theory and sources. Load when someone asks where the idea comes from, how it
differs from neighbouring techniques, or needs to argue the case to a team or a
manager.

## Canonical definition

Alistair Cockburn, *Crystal Clear* (2004):

> A Walking Skeleton is a tiny implementation of the system that performs a
> small end-to-end function. It need not use the final architecture, but it
> should link together the main architectural components. The architecture and
> the functionality can then evolve in parallel.

Freeman and Pryce, in *Growing Object-Oriented Software, Guided by Tests*,
restate it with the delivery clause made explicit: the thinnest possible slice
of real functionality that can be **automatically built, deployed and tested**
end-to-end. That clause is what most teams drop, and dropping it removes most of
the value.

Clint Shank, in *97 Things Every Software Architect Should Know*, adds the
growth instruction: once the skeleton is in place, put it on a workout program.
Keep it running while adding end-to-end functionality. The larger the system and
the more people involved, the more the technique pays.

## What it is not

| Not this | Difference |
| --- | --- |
| Prototype | Prototypes get thrown away. Slice code is production code you keep and grow. |
| MVP | An MVP answers *should we build this* and targets users. A thin slice answers *can we build this here* and targets the team. A slice can deliver zero user value and still succeed. |
| Proof of concept | A PoC answers "possible in principle". A slice answers "works in our real environment, deployed, monitored, integrated". |
| Spike | Timeboxed research, usually discarded. A slice ships. |
| Vertical slice | Close cousin. The skeleton is the first vertical slice, chosen for risk rather than value. |

Normal ordering: validate the need, then build the skeleton, then grow it into
the MVP.

## The family of names

- **Tracer bullet** (Hunt and Thomas, *The Pragmatic Programmer*): just enough
  code to confirm you are hitting the target, plus a repeatable feedback loop.
  Explicitly not throwaway. Used mostly for greenfield.
- **Steel thread** (popularised by Jade Rubick): a thin slice threading through
  every layer, "steel" because it becomes the foundation. Heavily used for
  migrations and service extraction. Repeated steel threads produce the
  strangler fig pattern.
- **Hello, production** (Pete Hodgson): the most extreme version. Deploy
  something with zero useful functionality to real production immediately. His
  rule: if the release has any useful functionality you are doing too much; if
  it is not responding to live traffic you are not doing enough.
- **Dancing skeleton** (Dan North): a skeleton plus an interface that lets
  people poke at it and experiment on the target architecture.
- **Skeleton on crutches** (Gojko Adzic): the inversion. Ship the user interface
  first on a deliberately cheap backend, then swap the backend to the target
  architecture behind continuous delivery without users noticing. Trades
  architectural proof for earlier real value. Choose it when reaching user
  feedback matters more than proving the stack.

## Why it works

**Front-loads risk.** Integration failures surface in week one rather than the
week before launch.

**Kills the cutover.** Big-bang integration is where projects die. Even a one
percent feature-flag rollout is still a cutover of everything at once. Threads
integrate continuously, so pain arrives in survivable doses.

**Unlocks parallel work.** Once the skeleton exists, different people can work
different parts without colliding. Even a solo builder benefits, because when
one stream blocks there is another to switch to.

**Forces the pipeline to exist.** It gets built when there is no feature
pressure. Teams that start this way tend to have anticlimactic launches, often
just a DNS change.

**Breaks silos.** Sometimes called an inverse Conway manoeuvre: the shape of the
first slice forces people from different teams to talk in week one.

**Makes estimates real.** After a skeleton the team has measured the friction
instead of guessing.

**For solo builders, it makes the project exist.** A project that lives only on
a laptop has no external reality, so skipping a weekend costs nothing. Once it
is live there is something to protect.

## Enterprise variant

In integration-heavy organizations, define the skeleton as: something that
proves all known integrations across people, process and technology for a given
scope. Layer it in this order:

1. Thin end-to-end technical path with build and test automation
2. An interface so stakeholders can interact with it
3. Instrumentation: logging, metrics, audit, analytics
4. Real integrations with the systems that already exist
5. Role-played use cases run through the real production environment, including
   the human steps

## When not to use it

- The need is unvalidated. Do discovery first.
- The architecture is proven and the team ships on it routinely.
- The change is a small feature in a well-understood system.
- The dominant risk is market, legal, or regulatory, not technical.

## Sources

- Alistair Cockburn, *Crystal Clear: A Human-Powered Methodology for Small
  Teams*, 2004
- Steve Freeman and Nat Pryce, *Growing Object-Oriented Software, Guided by
  Tests*, 2009
- Andy Hunt and Dave Thomas, *The Pragmatic Programmer*, tracer bullets chapter
- Clint Shank, "Start with a Walking Skeleton", *97 Things Every Software
  Architect Should Know*
- Gojko Adzic, "Forget the walking skeleton, put it on crutches" (2014),
  https://gojko.net/2014/06/09/forget-the-walking-skeleton-put-it-on-crutches/
- Jade Rubick, "Steel threads are a technique that will make you a better
  engineer" (2023), https://www.rubick.com/steel-threads/
- Pete Hodgson, "Hello, production" (2019),
  https://blog.thepete.net/blog/2019/10/04/hello-production/
- "Integration, integration, integration" (2019),
  https://www.defmyfunc.com/2019_10_18_walking_skeleton/
- Forsgren, Humble, Kim, *Accelerate*, 2018, on release tempo and organizational
  performance
