---
name: delight-audit
description: Judge whether an interface earns delight, using NN/g's distinction between surface delight (embellishment) and deep delight (which requires the product to be functional, reliable and usable first), plus Amber Case's calm technology principles for products that should sit in the periphery rather than demand attention. Use when asked to make something more delightful, add polish or personality, or evaluate whether animation and flourish are helping.
---

# Delight audit

Sources:
- Therese Fessenden, "A Theory of User Delight: Why Usability Is the Foundation for Delightful Experiences," Nielsen Norman Group (2017) — https://www.nngroup.com/articles/theory-user-delight/
- "The Role of Animation and Motion in UX," Nielsen Norman Group — https://www.nngroup.com/articles/animation-purpose-ux/
- Amber Case, Calm Technology — https://calmtech.com/

This is the judgment layer on top of the `impeccable` plugin, which handles execution (`polish`, `delight`, `animate`, `overdrive`). Use impeccable to build the flourish; use this to decide whether the flourish is the right thing to be building at all.

## The core idea

NN/g's finding, stated directly: *UI embellishments can only produce surface delight; deep delight can only be achieved in functional, reliable, and usable interfaces.* Delight has been stereotyped down to animation, mascots and snarky microcopy. Those produce a real but shallow and short-lived effect, and they cannot compensate for a product that is slow, confusing, or unreliable. A charming empty state on a flow the user cannot complete reads as mockery, not personality.

The ordering matters and it is not negotiable: functional, then reliable, then usable, then pleasurable. Flourish applied below that line is decoration on a problem. Flourish applied above it is what people remember.

## Checklist

**Before adding delight, check the foundation holds:**

1. **Functional** — does the thing do what the user came for, at all?
2. **Reliable** — does it work every time, including on slow networks and after errors?
3. **Usable** — can a user reach the outcome without being taught?

If any of those fail, the finding is "fix this first," not "add a spring animation."

**Then judge the delight itself:**

4. **Does the motion do work?** Animation should aid comprehension — show where a thing came from, maintain object continuity, direct attention to a change. Motion that only decorates costs time on every single use, and the cost compounds while the charm wears off.
5. **Does it survive repetition?** A flourish is experienced once by a designer and hundreds of times by a user. Delight that is charming on first encounter and irritating on the fiftieth is a net negative. Bias toward flourish at rare moments (first success, completion, recovery from error) over flourish on routine actions.
6. **Does it respect attention?** Case's calm technology argument: attention is the scarce resource, and good technology communicates from the periphery rather than demanding focus. A product that interrupts, badges, animates and notifies to seem lively is spending the user's attention to feel alive.
7. **Does it degrade honestly?** Respect `prefers-reduced-motion`. A delight that cannot be turned off is an imposition.
8. **Is the personality the product's, or a costume?** Voice that doesn't match what the product actually is reads as inauthentic faster than no voice at all.

## How to apply

Audit the foundation before the flourish, and say plainly when a request for "more delight" is actually a usability problem wearing a costume — that is the most useful finding this skill produces. When the foundation does hold, identify the specific rare moments worth investing in rather than spreading embellishment evenly, and hand the execution to the `impeccable` plugin.
