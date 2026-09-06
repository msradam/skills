---
name: error-handling-audit
description: Audit error handling for swallowed/ignored errors, lost context, duplicated handling logic, and errors logged and re-thrown at the same time. Use when writing code that can fail, or reviewing try/catch, error returns, or exception handling.
---

# Error handling audit

Source: Andrew Gerrand, "Error handling and Go," the Go blog (2011) — https://go.dev/blog/error-handling-and-go

Written for Go's explicit-error-value style, but the underlying discipline (check explicitly, preserve context, centralize repetition, decide once) applies regardless of language or whether the mechanism is return values or exceptions.

## The core idea

An error is a value carrying information about what went wrong, meant to be inspected and handled deliberately at the point where the program has enough context to decide what to do next — not a control-flow escape hatch to be caught generically far from where it happened and forgotten. Explicit, visible error checks at the call site (rather than hidden behind broad catch-all handlers) keep failure paths as legible as the success path, and make it obvious which calls can fail and what the code does about it.

## Checklist

When reviewing or writing error-handling code, flag:

1. **Swallowed errors** — an empty catch block, an ignored return value, or a catch that only logs and continues as if nothing happened when the caller actually needed to know.
2. **Lost context** — an error re-thrown or re-returned without adding what was being attempted when it occurred (wrap with context: what operation, what input, not just re-raising the original message).
3. **Log-and-throw** — the same error logged at the point it's caught *and* propagated further up to be logged again. Decide once where an error is actually handled (logged, and the decision made) versus where it's just passed along; don't do both at every layer.
4. **Generic catch-all** — catching a broad exception type/class when only a specific failure mode is actually expected and handleable; this hides genuine bugs by treating them the same as expected failures.
5. **Repeated boilerplate** — the same error-wrapping/logging/translation logic duplicated at every call site instead of centralized in one helper/middleware/decorator.
6. **Recoverable vs. fatal conflated** — a truly unrecoverable condition (can't proceed at all) handled the same way as a recoverable one (retry, fallback, surface to caller); fatal conditions should propagate to a point where the program can shut down cleanly, not be silently absorbed deep in a library.
7. **Caller-facing message vs. diagnostic detail** — a message a user/caller sees should be actionable and not leak internals; the full error detail (stack trace, underlying cause) belongs in logs/telemetry, not necessarily in what's surfaced to the caller.

## How to apply

Scan the target code's error paths against this checklist and fix directly: add missing context to a wrapped error, remove a redundant log-and-throw down to a single handling point, replace a swallowed error with an explicit decision (propagate, retry, or a justified intentional ignore with a comment explaining why it's safe to ignore). When the right handling strategy genuinely depends on product behavior the user hasn't specified (e.g., should this fail the whole request or degrade gracefully?), ask rather than guess.
