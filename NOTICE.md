# Sources

Every skill in this repository is original writing, distilled from — and citing — one specific, professionally-written, publicly available engineering guide. None of the source text is copied; each `SKILL.md` states its source at the top and links to the original for full context.

| Skill | Source | Author / Org |
|---|---|---|
| comment-audit | [Best practices for writing code comments](https://stackoverflow.blog/2021/12/23/best-practices-for-writing-code-comments/) | Ellen Spertus, Stack Overflow Blog (2021) |
| commit-message-audit | [How to Write a Git Commit Message](https://cbea.ms/git-commit/) | Chris Beams |
| code-review-audit | [How to do a code review](https://google.github.io/eng-practices/review/reviewer/) | Google Engineering Practices |
| test-pyramid-audit | [TestPyramid](https://martinfowler.com/bliki/TestPyramid.html) | Martin Fowler |
| refactoring-smells | [Refactoring catalog](https://refactoring.com/catalog/) | Martin Fowler |
| api-design-audit | [How to Design a Good API and Why it Matters](https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/32713.pdf) | Joshua Bloch, OOPSLA 2006 |
| error-handling-audit | [Error handling and Go](https://go.dev/blog/error-handling-and-go) | Andrew Gerrand, the Go blog (2011) |
| naming-audit | Rules for variable and class naming (as cited in Robert C. Martin's *Clean Code*) — [mirror](https://exelearning.org/wiki/OttingersNaming/) | Tim Ottinger |
| logging-audit | [Let's talk about logging](https://dave.cheney.net/2015/11/05/lets-talk-about-logging) | Dave Cheney |
| readme-audit | [Art of README](https://github.com/hackergrrl/art-of-readme) | Kira ("hackergrrl") |
| code-documentation-audit | [PEP 257](https://peps.python.org/pep-0257/) + [The Documentation System](https://docs.divio.com/documentation-system/) | Python Software Foundation; Divio |
| marketing-copy-audit | [An Introduction to Positioning](https://aprildunford.com/post/an-introduction-to-positioning) | April Dunford |

The three static-analysis skills (`lint-python`, `lint-go`, `lint-typescript`) aren't grounded in a writeup — they run real tooling instead: [ruff](https://docs.astral.sh/ruff/) + [mypy](https://mypy.readthedocs.io/) (Python), [go vet](https://pkg.go.dev/cmd/vet) + [golangci-lint](https://golangci-lint.run) (Go), and [tsc](https://www.typescriptlang.org/) + [ESLint](https://eslint.org)/[typescript-eslint](https://typescript-eslint.io) (TypeScript).

If you're one of the authors above and would prefer different attribution, or would rather this repository not cite your work, please open an issue.
