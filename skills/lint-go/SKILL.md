---
name: lint-go
description: Run deterministic static analysis on Go code using go vet (built into the toolchain) and golangci-lint (the standard meta-linter aggregating staticcheck, errcheck, ineffassign, unused, and more) — actual tool output, not stylistic opinion. Use when asked to lint, check, or clean up Go code, before committing Go changes, or when Go code quality needs verifying.
---

# Go static analysis

Tools: `go vet` (ships with the Go toolchain, no install needed) and [golangci-lint](https://golangci-lint.run) (the standard meta-linter; runs `staticcheck`, `errcheck`, `ineffassign`, `unused`, `govet`, and more under one command).

This skill runs real tools and reports their actual output — it does not substitute for them with general advice about "good Go style."

## Prerequisite

`go vet` requires only a working Go toolchain. `golangci-lint` requires separate installation (`go install github.com/golangci/golangci-lint/v2/cmd/golangci-lint@latest`, or the install script/binary per its docs) — check `golangci-lint --version` first; if it's missing, ask the user whether to install it rather than doing so unprompted, since it's a separate binary, not a language-builtin.

## Commands

- **Toolchain vet (always available)**: `go vet ./...`
- **Full lint (if golangci-lint is installed)**: `golangci-lint run` (equivalent to `golangci-lint run ./...` — recursive by default)
- **Autofix what golangci-lint can fix**: `golangci-lint run --fix`
- **Formatting**: `golangci-lint fmt` (or `gofmt -l .` to just list unformatted files)

## How to apply

1. Always run `go vet ./...` first — it needs no setup and catches real correctness bugs (suspicious struct tags, unreachable code, format-string/argument mismatches, lock-copying, etc.), not style opinions.
2. If `golangci-lint` is available, run `golangci-lint run` and report actual findings — file, line, linter name, message — not a paraphrased summary.
3. For findings golangci-lint can autofix, run `golangci-lint run --fix`, then re-run `golangci-lint run` to confirm what remains needs a manual decision.
4. Don't silence a finding with a blanket `//nolint` — if a finding is a genuine false positive, suppress the specific linter by name (`//nolint:errcheck`) with a comment explaining why, not a bare `//nolint` that also hides future, unrelated findings at that line.
5. Report a clean pass explicitly, and note plainly if `golangci-lint` wasn't available so only `go vet` ran — don't let a missing tool look like a clean full lint pass.
