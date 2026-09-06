---
name: lint-typescript
description: Run deterministic static analysis on TypeScript code using tsc (type checking) and eslint with typescript-eslint (linting) — actual tool output, not stylistic opinion. Use when asked to lint, check, or clean up TypeScript/JavaScript code, before committing changes, or when code quality needs verifying.
---

# TypeScript static analysis

Tools: `tsc --noEmit` (the TypeScript compiler's own type checker, run without emitting output) and [ESLint](https://eslint.org) with the [typescript-eslint](https://typescript-eslint.io) plugin — the standard combination; `tsc` catches type errors, ESLint catches everything else (unused vars, unsafe patterns, style/consistency rules).

This skill runs real tools and reports their actual output — it does not substitute for them with general advice about "good TypeScript style."

## Prerequisite

Requires `typescript`, `eslint`, `@eslint/js`, and `typescript-eslint` as devDependencies — none of these ship by default. Check `package.json`/`node_modules` first; if missing, ask the user whether to add them rather than installing unprompted. Current ESLint setups use flat config (`eslint.config.mjs` extending `tseslint.configs.recommended`); an older `.eslintrc` is still valid but check which the project actually uses before assuming.

## Commands

- **Type-check**: `npx tsc --noEmit` (or the project's own configured script, e.g. `npm run typecheck`, if one exists — prefer that so project-specific `tsconfig` paths are respected)
- **Lint, report only**: `npx eslint .`
- **Lint, autofix what's safely fixable**: `npx eslint . --fix`

## How to apply

1. Run `npx tsc --noEmit` first (or the project's typecheck script) and report actual type errors — file, line, error code (e.g. `TS2345`), message.
2. Run `npx eslint .` and report actual findings — file, line, rule name, message — not a paraphrased summary.
3. For findings ESLint can autofix, run `npx eslint . --fix` directly, then re-run `npx eslint .` to confirm what needs a manual decision (not everything is autofixable, especially type-aware rules).
4. Fix the actual type error at its source (correct the type, narrow a union, fix the mismatched argument) rather than reaching for `as any` or `@ts-ignore` — if a suppression is genuinely warranted, use `@ts-expect-error` with a comment explaining why, so it starts failing loudly again once the underlying issue is actually fixed upstream.
5. Report a clean pass explicitly for both tools, and note if either tool/config wasn't found so a skipped check doesn't read as a clean pass.
