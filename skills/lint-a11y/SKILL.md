---
name: lint-a11y
description: Run deterministic accessibility and performance checks against a running page using pa11y (axe + HTML_CodeSniffer rules) and Lighthouse — actual tool output, not design opinion. Use when asked to check accessibility, run an a11y audit, verify WCAG conformance, or measure page performance.
---

# Accessibility and performance checks

Tools: [pa11y](https://github.com/pa11y/pa11y) (bundles its own headless Chrome, and can run axe-core rules via `--runner axe`) and [Lighthouse](https://github.com/GoogleChrome/lighthouse) (accessibility plus performance in one pass).

This runs real tools against a real page and reports their actual findings. It does not replace design review — pair it with the `impeccable` plugin, which covers the subjective side (hierarchy, typography, motion, delight) and already carries Nielsen heuristics and WCAG contrast ratios.

## Prerequisite

Neither tool ships with Node. `pa11y` bundles Chrome, so it is the lower-friction of the two; `@axe-core/cli` is deliberately not used here because it needs a separately managed chromedriver. Check for them first, and ask before installing globally.

Both need a **reachable URL**. For a local app, start the dev server first and point at it; for a deployed page, hit it directly.

## Commands

- **Accessibility, axe ruleset**: `npx pa11y <url> --runner axe --reporter json`
- **Accessibility, both rulesets** (broader coverage): `npx pa11y <url> --runner axe --runner htmlcs`
- **Specific standard**: `npx pa11y <url> --standard WCAG2AA`
- **Fail above a finding count** (for CI): `npx pa11y <url> --threshold 0`
- **Multiple URLs from config**: `npx pa11y-ci` (reads `.pa11yci`)
- **Accessibility + performance**: `npx lighthouse <url> --only-categories=accessibility,performance --output=json --output-path=./lh.json --quiet --chrome-flags="--headless"`

Lighthouse needs Node 22+. It runs entirely locally and does not send results anywhere.

## How to apply

1. Confirm the target URL is actually serving before running — a failed page load reports as zero violations, which reads like a pass.
2. Run pa11y with `--runner axe` and report the actual findings: selector, WCAG criterion, and message. Do not paraphrase into a vague summary.
3. Fix the underlying markup — a missing label, an unlabelled control, a contrast failure, a heading level skip. Never suppress a rule to make output green.
4. Re-run after fixing to confirm the finding is gone rather than assuming.
5. For contrast failures, fix the token in the design system rather than the one component, when a shared token is the source.
6. Report a clean pass explicitly, and say plainly if a tool was missing or the URL was unreachable, so a skipped check never reads as a passing one.

Automated tools catch roughly the machine-checkable subset of accessibility — valid markup, contrast, names and roles. They cannot tell you whether the keyboard order makes sense or whether a screen-reader user can actually complete the task. Say so rather than reporting a clean automated run as "accessible".
