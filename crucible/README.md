# Crucible

You are the worst person to judge your own idea, and the model you ask
is the second worst — it's built to agree with you. Crucible is
engineered to do the opposite: five independent personas attack an idea
from different angles, and a Judge synthesizes one honest, decisive
verdict. Run it *before* sinking time or money into building the wrong
thing.

Built to the open [Agent Skills](https://agentskills.io) standard —
one plain-markdown `SKILL.md`, no scripts, no dependencies. Tested on
Claude Code; because it's pure instructions, it runs anywhere — worst
case, paste the body into a rules file (see [`INSTALL.md`](./INSTALL.md)).

## What it does

You give it an idea in a sentence or two (plus, if you have them, the
buyer, the business model, and your unfair advantage). Then:

1. **The council** — five personas judge the *same* brief,
   **independently** (none sees another's output — that independence
   is the whole design):
   - **Contrarian** — assumes it fails; finds the fastest way it dies.
   - **Expansionist** — the strongest honest bull case and the 10x
     version.
   - **Logician** — first principles only; do the mechanism and the
     incentives actually hold?
   - **Researcher** — real competitors, substitutes, and comparable
     pricing (cites sources when web search is available; labels
     everything "unverified" when it isn't).
   - **Buyer** — role-plays your exact target customer, honest and
     skeptical: would they actually pay?
2. **The Judge** — resolves the tension between them into one call:
   **GO / RESHAPE / KILL**, with the biggest risk, the biggest upside,
   a money read, and — the most important output — the cheapest
   **48-hour, near-zero-build test** that tells you whether you're
   right without building anything.

The friction is the product. No persona hedges or softens. Veto floors
stop a broken mechanism or a customer-won't-pay signal from being
outvoted into a GO, and an explicit anti-sycophancy check runs before
the verdict is finalized.

## Why

Every founder's instinct is to protect the idea; every generic AI's
instinct is to encourage the person in front of it. Both push the same
direction — toward building. The expensive mistakes happen when nobody
in the room is trying to kill the idea *cheaply*, on purpose, before
the build. Crucible is that room.

## Example

[`example/worked-example.md`](./example/worked-example.md) — a full
run on a sample idea: the brief, all five personas, the Judge's
verdict, and the falsifiable 48-hour test it lands on.

## Status

In use. This one has no 60-day kill criterion like the historian —
it's a decision aid, not a habit to falsify — but it earns its keep by
one standard: the 48-hour test it produces must be *behavioral*
(measures what people do, not what they say), *falsifiable* (a
pass/fail threshold declared before running it), and executable
without building the product. A verdict that doesn't end in a test
that meets that bar is a Crucible failure, not a founder failure.
