# skills

Autonomous software-engineering skills for Claude Code (and other agent harnesses that read `SKILL.md`), each authored from one specific, well-regarded, professionally-written engineering guide rather than generic advice. See [NOTICE.md](NOTICE.md) for full sourcing.

Unlike a conversational co-authoring workflow, these are designed to scan and fix directly when triggered — audit, then apply the fix, asking only when a decision genuinely requires the user's input.

## Skills

**`swe-writeups`** — code-quality audits, each grounded in one writeup:
- **comment-audit** — comments should explain why, not restate the code (Ellen Spertus / Stack Overflow Blog)
- **commit-message-audit** — the seven-rule commit message standard (Chris Beams)
- **code-review-audit** — how to review and phrase feedback well (Google Engineering Practices)
- **test-pyramid-audit** — the right mix of unit/integration/e2e tests (Martin Fowler)
- **refactoring-smells** — named code smells mapped to named refactorings (Martin Fowler)
- **api-design-audit** — easy to use correctly, hard to misuse (Joshua Bloch)
- **error-handling-audit** — explicit, contextual, non-duplicated error handling (Andrew Gerrand / the Go blog)
- **naming-audit** — pronounceable, searchable, consistent identifier names (Tim Ottinger)
- **logging-audit** — two log levels, not six (Dave Cheney)

**`writing-skills`** — docs and marketing copy, each grounded in one writeup:
- **readme-audit** — broad-to-specific "cognitive funneling" (Kira / Art of README)
- **code-documentation-audit** — docstring mechanics (PEP 257) + picking the right doc type (Divio)
- **marketing-copy-audit** — clear positioning before clear copy (April Dunford)

**`static-analysis`** — deterministic linting, no writeup needed, runs real tools:
- **lint-python** — ruff (lint + format) + mypy (types)
- **lint-go** — go vet + golangci-lint
- **lint-typescript** — tsc (types) + eslint (lint)

## Install (Claude Code)

```
/plugin marketplace add msradam/skills
/plugin install swe-writeups@msradam-skills
/plugin install writing-skills@msradam-skills
/plugin install static-analysis@msradam-skills
```

## License

MIT — see [LICENSE](LICENSE). Source writeups this repo is distilled from remain the copyright of their respective authors; see [NOTICE.md](NOTICE.md).
