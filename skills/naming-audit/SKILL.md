---
name: naming-audit
description: Audit identifier names (variables, functions, classes) for pronounceability, searchability, consistent vocabulary, and meaningless differentiation like data1/data2. Use when reviewing code for readability, naming a new identifier, or asked whether a name is good.
---

# Naming audit

Source: Tim Ottinger, rules for variable and class naming (widely cited, e.g. in Robert C. Martin's *Clean Code*) — https://exelearning.org/wiki/OttingersNaming/ (mirror of Ottinger's original post)

## The core idea

A name is read far more often than it's written, and it's the only documentation most code ever gets — a reader forms their understanding of what something is and does from its name before they read a single line of its body. A name that requires the reader to already know the answer (a single letter, an abbreviation only the author understands, a name that describes the type instead of the purpose) fails at that one job. Naming well is not a stylistic nicety; it's the cheapest, highest-leverage form of documentation available, and it's free to keep in sync because it's part of the code itself.

## Checklist

1. **Pronounceable and searchable** — can you say it out loud in a discussion, and can you grep for it without false positives? Avoid names so short or generic (`d`, `tmp`, `x`) that they can't be searched for meaningfully, except for genuinely tiny scopes (a loop index is fine).
2. **No encoded type information** — avoid Hungarian-notation-style prefixes (`strName`, `iCount`) or baking the type into the name when the type system already tracks the type; name the *purpose*, not the type.
3. **Consistent vocabulary** — pick one verb per concept across the codebase (don't mix `fetch`/`retrieve`/`get` for the same kind of operation, or `remove`/`delete`/`erase` for the same kind of action) so a reader can predict a name from the concept alone.
4. **No disinformation** — a name shouldn't imply something false about what it holds (calling something `accountList` when it's actually a set or map; calling a mutable object `frozenConfig` if it isn't).
5. **Meaningful distinction, not noise** — `data1`/`data2`, `productInfo`, `theManager` — words added only to satisfy a compiler/linter or to make two similar names different, without adding real meaning. Each name should tell the reader what's actually different about it.
6. **Nouns for things, verbs for actions** — classes/objects get noun phrases (`InvoiceGenerator`, not `GenerateInvoice`); methods/functions get verb phrases (`generateInvoice`, not `invoiceGenerator`).
7. **Length matches scope** — a name's length should scale with how far it travels and how long it lives: a loop counter used for three lines can be `i`; a field on a class used across a whole module needs a name that carries its meaning on its own.

## How to apply

Scan identifiers in the target scope against this checklist. When proposing a rename, check all references in the accessible codebase and update them together (a rename that only touches the declaration is a name in disguise for a bug) — use a project-wide search before applying `replace_all`, and flag renames that cross a public API boundary as needing more care (see api-design-audit) since external callers may depend on the old name.
