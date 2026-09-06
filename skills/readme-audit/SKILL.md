---
name: readme-audit
description: Audit or write a README against the "cognitive funneling" principle — broad to specific ordering so a skimming reader gets the gist in seconds and only drills in as far as they need. Use when writing a new README, reviewing an existing one, or asked whether a README is clear/complete.
---

# README audit

Source: Kira ("hackergrrl"), *Art of README* — https://github.com/hackergrrl/art-of-readme

## The core idea

A README's job is to let someone understand what a project is and whether they need it, without reading the source. Most READMEs fail not by omitting information but by ordering it wrong: a reader arrives knowing nothing and needing almost none of the detail immediately available, so a README that opens with installation minutiae or a long history before saying what the thing does loses that reader before they get to the part that would have hooked them.

The fix is **cognitive funneling**: order sections broad-to-specific, so a five-second skim answers "what is this," a thirty-second skim answers "is this what I need and how do I try it," and only a reader who's still interested continues into API detail, configuration, and contribution guidelines. Every reader gets exactly as much depth as they need and stops exactly where their interest ends — nobody is forced past the point they'd have bailed anyway.

## Checklist

1. **Name and one-line description first** — before anything else, what is this and what does it do, in one sentence a stranger to the domain could parse.
2. **Usage example early** — a minimal, copy-pasteable example of the thing actually working, before installation instructions. A reader deciding whether to use something wants to see it work before they invest in installing it.
3. **Broad-to-specific ordering** — description → quick example → install → detailed usage/API → configuration → contributing → license. Flag sections that bury a broad-audience concern (like "what does this do") beneath a narrow one (like a changelog or a contributor's guide).
4. **No forced reading** — a reader who only wants to know "does this solve my problem" shouldn't have to scroll past API reference detail to find out; a reader who wants full API detail shouldn't have to reconstruct it from scattered examples.
5. **Badges/links serve discoverability, not decoration** — build status, license, package registry links belong near the top only if they help a reader decide "is this legitimate/maintained," not as visual clutter.
6. **Nothing critical only in the source** — anything a user genuinely needs to use the project correctly (required config, non-obvious constraints, common pitfalls) belongs in the README, not left for someone to discover by reading the code.

## How to apply

When writing a new README, draft it in the broad-to-specific order directly. When auditing an existing one, reorder sections that violate the funnel, add a usage example if installation instructions come first with no example, and flag (or move) any critical information that's currently only inferable from source code.
