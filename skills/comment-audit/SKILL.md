---
name: comment-audit
description: Audit and fix code comments — flag comments that restate the code instead of explaining why, stale comments that no longer match the code, comments used to excuse unclear code instead of fixing it, and undocumented TODOs. Use when asked to review, audit, clean up, or write comments, or when comments look suspicious while editing nearby code. Act autonomously — fix directly, don't just narrate findings.
---

# Comment audit

Source: Ellen Spertus, "Best practices for writing code comments," Stack Overflow Blog (2021) — https://stackoverflow.blog/2021/12/23/best-practices-for-writing-code-comments/

## The core idea

Code already says *how*. A comment earns its place only by saying something the code cannot: *why*. A comment that just narrates the next line in English is a tax on every future reader — it can drift out of sync with the code, and until it does it added nothing. When a comment is doing real work, it's usually because the code alone would leave a real question unanswered: why this approach and not the obvious one, why this magic number, what this workaround is compensating for, what a caller must not assume.

The corollary that matters most in practice: **if a comment is hard to write clearly, that is a signal the code needs work, not the comment.** Reaching for a comment to explain confusing code is treating a symptom. The fix is usually a rename, an extracted function with a name that carries the meaning, or breaking up the logic — not a longer comment.

## Checklist

When auditing comments in a file or diff, flag each of these:

1. **Restates the code** — `// increment i` above `i++`, `// loop over users` above `for user in users`. Delete; the code already reads that way.
2. **Excuses unclear code** — a comment explaining what a cryptically-named variable or tangled conditional *actually* does. Prefer renaming/refactoring over commenting; only fall back to a comment if the refactor genuinely can't be done now (and say why not).
3. **Missing where it's earned** — non-obvious algorithm choices, workarounds for a specific bug or platform quirk, business-rule-driven magic numbers/thresholds, anything a reasonable reader would ask "wait, why?" about.
4. **Stale** — a comment describing behavior the code next to it no longer has (check comments against the actual current logic, not just their own wording).
5. **Undated/untracked TODO or FIXME** — flag TODOs with no issue reference or owner as ambiguous debt; suggest linking to a tracked issue or removing if it's stale.
6. **Public API docs conflated with implementation comments** — docstrings on public functions/classes should describe the contract (inputs, outputs, preconditions, side effects) for a caller who can't see the body, not narrate the implementation.

## How to apply

Scan the comments in the target file(s) or diff. For each violation, apply the fix directly (delete the redundant comment, rewrite the comment to explain why, or refactor the code and remove the now-unnecessary comment) rather than just listing problems — this skill runs autonomously, not as a back-and-forth review. Only stop to ask the user when a fix would require a decision only they can make (e.g., whether a TODO is still relevant, or which of two refactor directions they prefer).
