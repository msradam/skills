---
name: refactoring-smells
description: Detect named code smells (long function, duplicated code, large class, long parameter list, feature envy, primitive obsession, speculative generality, dead code) and apply the matching named refactoring from Martin Fowler's catalog. Use when asked to clean up, refactor, or simplify existing code, or when a function/class feels harder to change than it should.
---

# Refactoring smells audit

Source: Martin Fowler, refactoring catalog — https://refactoring.com/catalog/

## The core idea

A "code smell" is a surface symptom that usually points to a specific, well-understood structural problem — not a vague sense that code is bad, but a recognizable pattern with a named fix. Treating smells as a catalog (symptom → named refactoring) turns "this code feels off" into a concrete, mechanical, low-risk transformation, applied in small steps that keep the code working at every intermediate point rather than a risky rewrite.

Refactoring changes structure without changing observable behavior. If a "cleanup" changes what the code does, it isn't a refactoring — it's a rewrite, and it needs the scrutiny (and tests) a behavior change deserves.

## Smell → refactoring

| Smell | What it looks like | Typical fix |
|---|---|---|
| Long function | A function that does several distinct things in sequence | Extract Function for each cohesive chunk |
| Duplicated code | Same or near-same logic in multiple places | Extract Function/Class and call it from both sites |
| Large class / God object | A class that owns too many unrelated responsibilities | Extract Class to split responsibilities |
| Long parameter list | A function taking many loosely-related parameters | Introduce Parameter Object, or split the function |
| Feature envy | A method that mostly operates on another object's data | Move Method to the class whose data it actually uses |
| Primitive obsession | Using raw strings/ints where a small domain type would carry meaning and validation | Replace Primitive with Object (e.g., a `Money` or `EmailAddress` type instead of a bare string) |
| Repeated conditional on type/state | The same `if`/`switch` on a type tag appears in multiple places | Replace Conditional with Polymorphism |
| Speculative generality | Abstraction, parameters, or hooks built for a use case that doesn't exist yet | Remove the unused generality; add it back when a real second use case appears |
| Dead code | Code no longer called from anywhere reachable | Remove Dead Code |

This table is illustrative, not exhaustive — the full catalog covers many more named refactorings for other structural problems.

## How to apply

Scan the target code for these smells and apply the matching refactoring directly, in small verifiable steps, preserving behavior exactly. Before refactoring, check that adequate tests exist to catch a behavior change; if not, say so before proceeding, since a refactor without a safety net is a rewrite in disguise. Do not introduce new abstraction for a problem that only has one instance today (that's speculative generality in the other direction) — this pairs with the minimalism/anti-bloat discipline in the ponytail skill.
