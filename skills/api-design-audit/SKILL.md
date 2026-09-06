---
name: api-design-audit
description: Review a public API, interface, or function signature against Joshua Bloch's API design principles — easy to use correctly, hard to misuse, minimal surface area, and consistent. Use when designing a new public interface/library/function signature, or reviewing one someone else proposed.
---

# API design audit

Source: Joshua Bloch, "How to Design a Good API and Why it Matters," OOPSLA 2006 — https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/32713.pdf

## The core idea

An API is a contract with every future caller, and unlike internal code, it's far more expensive to change once callers depend on it — so design effort spent before the first release pays off many times over. Bloch's central framing: a good API should be easy to use even without reading documentation, and hard to use incorrectly. If callers keep misusing an API the same way, that's a design defect, not a documentation gap — the fix is to change the API so the mistake becomes impossible or a compile-time/type error, not to add a warning in the docs.

## Checklist

When designing or reviewing a public API/interface/function signature:

1. **Easy to use correctly, hard to misuse** — can a caller who hasn't read the docs get it right by guessing? Can they get it wrong in a way the type system or a validity check should have caught instead?
2. **Minimal surface area** — expose the fewest public members/methods/parameters that solve the problem. Every public element is a permanent commitment; when in doubt, leave it out (it's easy to add later, hard to remove).
3. **Consistency** — same naming conventions, parameter order, and behavior patterns across the whole API. A caller who learns one part should be able to predict the rest.
4. **Don't make the caller do what the module could do** — if the API can validate, default, or compute something internally, don't push that burden onto every caller.
5. **Fail fast** — validate inputs and reject invalid state as early as possible (ideally at the call that introduced it), not deep inside unrelated logic where the failure is confusing to trace back.
6. **Favor immutability** — where the domain allows it, immutable objects are easier to reason about, share safely, and cannot be corrupted after handoff.
7. **Documented and tested from a caller's perspective** — real usage examples, and tests that exercise the API the way a consumer actually would, not just the way the implementer wrote it.

## How to apply

When designing a new interface, propose the signature/shape directly against this checklist rather than the first version that comes to mind, and flag tradeoffs explicitly (e.g., "this parameter could be optional with a sensible default instead of required"). When reviewing an existing API, point out concrete misuse scenarios the current shape allows and propose the specific signature change that would make that misuse impossible or a type error — don't stop at "this could be clearer."
