---
name: commit-message-audit
description: Write or fix git commit messages against Chris Beams' seven-rule standard — proper subject/body separation, imperative mood, line-wrapping, and explaining why a change was made rather than what changed. Use when drafting a commit message, reviewing one before committing, or cleaning up commit history/messages.
---

# Commit message audit

Source: Chris Beams, "How to Write a Git Commit Message" — https://cbea.ms/git-commit/

## The core idea

A commit message is documentation, not a log line. `git log`, `git blame`, and every future reader of the history depend on messages that read as a coherent narrative of *why* the codebase changed — the diff already shows *what* changed line by line. A commit message that just restates the diff in prose ("update file.py", "fix bug", "changes per review") throws away the one piece of context the diff itself cannot carry: the reasoning.

## The seven rules

1. Separate subject from body with a blank line.
2. Limit the subject line to ~50 characters.
3. Capitalize the subject line.
4. Do not end the subject line with a period.
5. Use the imperative mood in the subject ("Fix bug," not "Fixed bug" or "Fixes bug" — a good test: the subject should complete the sentence "If applied, this commit will ___").
6. Wrap the body at ~72 characters.
7. Use the body to explain *what* and *why*, not *how* — the diff already shows how.

## How to apply

- **Drafting a new message**: after making the change, write the subject in imperative mood summarizing the change, then a blank line, then a body covering: what problem existed before, why this approach was chosen (especially if a simpler one was rejected), and any consequence the reader should know (behavior change, follow-up needed, etc.). Skip the body only for changes truly too small to need one.
- **Reviewing an existing message** (e.g., before `git commit` or when asked to check one): apply the seven rules directly — reword the subject to imperative mood, split into subject/body if missing, trim to line-length limits, and flag (or rewrite) a body that only restates the diff instead of explaining reasoning. Fix directly rather than just listing violations.
- Never fabricate a "why" that isn't grounded in the actual change or in context the user gave — if the reasoning isn't evident from the diff or conversation, ask rather than invent a plausible-sounding justification.
