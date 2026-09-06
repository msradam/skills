---
name: lint-python
description: Run deterministic static analysis on Python code using ruff (linting + formatting) and mypy (type checking) — actual tool output, not stylistic opinion. Use when asked to lint, check, or clean up Python code, before committing Python changes, or when Python code quality needs verifying.
---

# Python static analysis

Tools: [ruff](https://docs.astral.sh/ruff/) (Astral) — unified linter and formatter, the current de facto standard, replacing the older Flake8/Black/isort/pyupgrade/pydocstyle combination — and [mypy](https://mypy.readthedocs.io/), the standard static type checker.

This skill runs real tools and reports their actual output — it does not substitute for them with general advice about "good Python style."

## Prerequisite

Both tools must already be available in the project (as a dependency, or installed via `pip`/`pipx`/`uv`). Check first (`ruff --version`, `mypy --version`, or look for them in `pyproject.toml`/`requirements*.txt`); if neither is present, ask the user whether to add them as a dev dependency rather than installing globally without asking.

## Commands

- **Lint, report only**: `ruff check .`
- **Lint, autofix what's safely fixable**: `ruff check --fix .`
- **Format**: `ruff format .` (or `ruff format --check .` to report without modifying files)
- **Type-check**: `mypy .` (or the specific package/directory, e.g. `mypy src/`)

## How to apply

1. Run `ruff check .` and `mypy .` (or the relevant subdirectory) and report the actual findings — file, line, rule/error code, message — don't paraphrase into vague summary.
2. For lint findings ruff can autofix, run `ruff check --fix .` directly rather than manually editing to match; then re-run `ruff check .` to confirm clean, since not every finding is autofixable.
3. Run `ruff format .` to normalize formatting, unless the project has an existing formatter config that conflicts (check `pyproject.toml` for `[tool.ruff]`/`[tool.black]` sections first).
4. For mypy errors, fix the actual type issue (add/correct annotations, narrow a type, handle an `Optional`) rather than suppressing with `# type: ignore` — reserve `# type: ignore[code]` (always with the specific error code, never bare) for cases where the type checker is genuinely wrong, and say why in a comment.
5. Report a clean pass explicitly ("ruff: 0 issues, mypy: 0 errors") so the user knows the check actually ran rather than silently passing because the tool wasn't installed.
