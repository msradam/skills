---
name: logging-audit
description: Audit logging calls against Dave Cheney's argument for collapsing severity levels to just Debug (developer-facing) and Info (operator-facing, always visible) — flag level sprawl, error-level logs at points that are just informational, and fatal exits buried deep in library code. Use when adding logging to code, or reviewing existing logging statements.
---

# Logging audit

Source: Dave Cheney, "Let's talk about logging" — https://dave.cheney.net/2015/11/05/lets-talk-about-logging

This is one strong, well-reasoned position in an area with real disagreement across teams and ecosystems, not a universal consensus — apply it as a default and defer to an existing project's established logging conventions where they differ.

## The core idea

Cheney argues most logging APIs offer too many severity levels (trace/debug/info/warn/error/fatal), and in practice teams can't agree where the boundaries are — "warn" versus "error" ends up decided inconsistently line by line, and consumers of logs can't reliably filter by a taxonomy nobody applies the same way twice. His proposal: collapse to two levels defined by *audience*, not *severity*:

- **Debug** — for developers diagnosing a specific problem; verbose, off by default, safe to be noisy.
- **Info** — for operators/end users; always visible, meant to be readable without special tooling, kept to what actually matters operationally.

A handled error is not automatically "Error" severity — if the code caught it and dealt with it (retried, fell back, returned a clean result to the caller), that's informational at most, not a distinct alarm level. A condition the program truly cannot recover from should propagate up to the top of the program (e.g., `main`) where it can be handled with proper cleanup and a clean exit — not resolved by calling an exit/fatal function deep inside a library, which denies every caller the chance to decide what "fatal" means for them.

## Checklist

1. **Level sprawl** — more than two meaningfully-distinguished levels in active use; check whether "warn" entries are really just Debug or Info in disguise.
2. **Handled errors logged as errors** — an error that was caught and successfully dealt with, logged at a severity implying something is still wrong.
3. **Fatal calls buried in library code** — `os.Exit`, `log.Fatal`, `process.exit`, or equivalent, called from deep inside reusable/library code rather than from the top-level entry point, robbing callers of the chance to shut down cleanly.
4. **Noise that isn't operationally actionable** — Info-level logs that don't help an operator understand system health or make a decision, cluttering the always-visible stream.
5. **Missing context on Debug logs** — developer-facing logs that don't carry enough state (inputs, relevant IDs) to actually diagnose the problem they're meant for.

## How to apply

Review logging statements in the target code against this checklist. Where a project already has an established logging convention (its own level taxonomy, a structured-logging schema, a house style), follow the existing convention rather than forcing this model on top of it — flag the tension to the user instead of silently overriding established practice. Otherwise, apply Cheney's two-level model directly: reclassify or remove sprawled levels, move a buried fatal exit up to the program's entry point, and demote logged-but-handled errors to Debug.
