---
name: code-review-audit
description: Apply Google's Engineering Practices standards for how a code review should be conducted and communicated — what to actually check for, how to phrase feedback so it lands well, and when a nit should block a merge versus not. Use when reviewing a PR/diff/CL, or writing review comments, especially to check the tone and prioritization of feedback rather than just hunting for bugs.
---

# Code review audit

Source: Google Engineering Practices, "How to do a code review" — https://google.github.io/eng-practices/review/reviewer/

This complements a correctness-focused review (bug-hunting) — it's about *how* review is conducted and communicated, not a substitute for one.

## The core idea

A review's job is to make sure the overall code health of the codebase improves with every change, not to force every change into the reviewer's personal preferred style. Reviewers should approve a change once it definitely improves the codebase, even if it isn't perfect — perfection is not the standard, and demanding it stalls good changes over trivia. Feedback quality matters as much as feedback accuracy: a technically correct comment delivered badly damages the review process as a tool.

## Checklist

When reviewing a diff/PR, or writing review comments, check for:

1. **Design** — does the overall approach make sense, does it fit the existing system, is it over- or under-engineered for the problem?
2. **Functionality** — does the change do what the author intended, and is that what users/callers actually need? Check edge cases the author may not have considered.
3. **Complexity** — could a reader understand this easily? Flag code that's more complex than the problem requires.
4. **Tests** — are there appropriate unit/integration tests, and do they actually verify behavior (not just execute the code)?
5. **Naming and comments** — clear names, comments that explain why (see the comment-audit skill).
6. **Consistency with existing style** — matches the codebase's conventions, even where the reviewer might personally prefer otherwise.
7. **Scope** — is this change doing one coherent thing, or should it be split?

## How to phrase feedback

- Comment on the code, not the author ("this function doesn't handle X" not "you forgot X").
- Explain *why*, don't just assert a preference — a reviewer's reasoning helps the author generalize the lesson.
- Distinguish blocking issues from nits explicitly (e.g., prefix optional suggestions with "Nit:") so the author knows what must change before merge versus what's optional.
- Ask questions when intent is unclear rather than asserting the author is wrong ("What happens if this list is empty?" rather than "This breaks on empty lists" when you're not certain).
- Balance the cost of the review round-trip against the value of the requested change — don't block on stylistic preference alone.

## How to apply

When asked to review a PR/diff, work through the checklist and draft review comments that follow the phrasing guidance above — write them ready to post, don't just summarize internally. When asked to review draft review comments someone else wrote, check tone (does it read as attacking the person?), check that blocking vs. non-blocking is clear, and rewrite directly where it isn't.
