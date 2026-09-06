# skills

Autonomous software-engineering skills for Claude Code (and other agent harnesses that read `SKILL.md`), each authored from one specific, well-regarded, professionally-written engineering guide rather than generic advice. See [NOTICE.md](NOTICE.md) for full sourcing.

Unlike a conversational co-authoring workflow, these are designed to scan and fix directly when triggered — audit, then apply the fix, asking only when a decision genuinely requires the user's input.

## Skills

- **comment-audit** — comments should explain why, not restate the code (Ellen Spertus / Stack Overflow Blog)
- **commit-message-audit** — the seven-rule commit message standard (Chris Beams)
- **code-review-audit** — how to review and phrase feedback well (Google Engineering Practices)
- **test-pyramid-audit** — the right mix of unit/integration/e2e tests (Martin Fowler)
- **refactoring-smells** — named code smells mapped to named refactorings (Martin Fowler)
- **api-design-audit** — easy to use correctly, hard to misuse (Joshua Bloch)
- **error-handling-audit** — explicit, contextual, non-duplicated error handling (Andrew Gerrand / the Go blog)
- **naming-audit** — pronounceable, searchable, consistent identifier names (Tim Ottinger)
- **logging-audit** — two log levels, not six (Dave Cheney)

## Install (Claude Code)

```
/plugin marketplace add msradam/skills
/plugin install swe-writeups@msradam-skills
```

## License

MIT — see [LICENSE](LICENSE). Source writeups this repo is distilled from remain the copyright of their respective authors; see [NOTICE.md](NOTICE.md).
