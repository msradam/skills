---
name: code-documentation-audit
description: Audit or write inline code documentation (docstrings, doc comments, reference/API docs) against PEP 257's docstring conventions and the Divio documentation system's four document types. Use when writing docstrings, reviewing whether documentation is complete, or deciding what kind of document (tutorial, how-to, reference, explanation) a piece of documentation should be.
---

# Code documentation audit

Sources:
- PEP 257, docstring conventions (Python Software Foundation) — https://peps.python.org/pep-0257/
- Divio, "The Documentation System" — https://docs.divio.com/documentation-system/

PEP 257 is Python-specific in mechanics but its principles for docstrings generalize to any language's doc-comment convention (JSDoc, Go doc comments, Rustdoc, etc.). Divio's framework applies to any documentation, inline or standalone.

## Docstring mechanics (PEP 257)

1. **One-line summary first** — a single imperative-mood sentence summarizing what the function/class does ("Return the sum," not "Returns the sum" or "This function returns the sum"), on its own line.
2. **Blank line, then elaboration** — for anything beyond a one-liner: summary, blank line, then details covering arguments, return value, exceptions/errors raised, and any side effects or preconditions a caller can't see from the signature.
3. **Describes the contract, not the implementation** — a docstring should tell a caller what they need to know to use the function correctly without reading its body: what it does, what it assumes, what it promises. Implementation detail belongs in inline comments (see the comment-audit skill), not the docstring.
4. **Consistent indentation and format** — docstrings should follow the same structural convention throughout a codebase (whichever the project has already adopted — Google-style, NumPy-style, reST, etc.) rather than mixing styles function to function.

## Which type of document is this? (Divio)

Documentation fails when a single document tries to do two of these four jobs at once — each has a different audience and a different job:

| Type | Audience need | Job |
|---|---|---|
| Tutorial | "I'm new, walk me through it" | Learning-oriented: a guaranteed-to-work path to a first success |
| How-to guide | "I know the basics, help me do this specific thing" | Task-oriented: steps to a specific goal |
| Reference | "I need the exact facts" | Information-oriented: complete, accurate, and boring — no narrative |
| Explanation | "I want to understand why" | Understanding-oriented: context, rationale, design decisions |

A reference page that stops to teach concepts loses the reader trying to look up one fact fast. A tutorial that tries to be comprehensive instead of a guaranteed-to-succeed path loses the beginner it's for. Mixing types is the most common structural documentation mistake.

## How to apply

When writing a docstring, follow the PEP 257 structure directly (one-line summary, blank line, args/returns/raises) and match whatever docstring style the surrounding codebase already uses. When auditing existing documentation — a docstring, a wiki page, a docs site — first identify which of the four Divio types it's trying to be (or should be), then check it stays in that lane; if a document is doing two jobs, recommend or make the split into two documents rather than trying to serve both audiences from one page.
