---
name: test-pyramid-audit
description: Audit a test suite's shape against Martin Fowler's test pyramid — flag over-reliance on slow, brittle end-to-end/UI tests when a cheaper unit test would catch the same regression, and recommend or write the missing lower-level test. Use when reviewing test coverage, adding tests for a bug fix, or asked whether a test suite is well-structured.
---

# Test pyramid audit

Source: Martin Fowler, "TestPyramid" — https://martinfowler.com/bliki/TestPyramid.html

## The core idea

Tests at different levels trade off speed and confidence differently. Unit tests are fast, cheap to write, and pinpoint failures precisely — but only prove a piece works in isolation. End-to-end/UI tests give the most confidence that the whole system actually works together, but they're slow, expensive to write and maintain, and often flaky, so a large suite of them is costly to keep green. The pyramid shape — many unit tests, fewer service/integration tests, very few end-to-end tests — gets most of the confidence at the lowest cost, because most bugs are logic bugs that a unit test catches just as well as an end-to-end test would, for a fraction of the runtime and maintenance burden.

The actionable consequence: **when an end-to-end test catches a regression, that's a signal a unit test should exist to catch the same class of bug next time** — the end-to-end test did its job once, but leaving it as the only defense means every future regression of that kind costs a full slow test-suite run (or worse, ships) instead of failing fast in milliseconds.

## Checklist

When auditing a test suite or a set of tests added for a change:

1. **Shape** — roughly, is there a broad base of unit tests, a smaller layer of integration/service tests, and a thin top of end-to-end tests? A suite that's inverted (mostly slow end-to-end tests, few unit tests) is a red flag.
2. **Redundant coverage at the wrong level** — logic that's fully exercised by an end-to-end test but has no corresponding unit test, meaning a regression there is caught late and slowly instead of early and fast.
3. **Bug fixes without a matching unit test** — when a bug was found via manual testing, an end-to-end test, or a production incident, check whether a fast unit test was added at the actual point of failure, not just a test at whatever level happened to catch it.
4. **Flaky or slow tests standing in for what a unit test could verify** — tests that hit real network/filesystem/timing when the logic under test doesn't actually need it.

## How to apply

When asked to review test coverage, categorize existing tests by level and report the shape plainly (e.g., "12 e2e tests, 3 integration tests, 4 unit tests — inverted pyramid"). When a bug fix or PR adds only a higher-level test for a lower-level bug, write the missing unit test directly rather than only recommending it. Don't recommend deleting existing end-to-end coverage — the fix is to add the cheaper test underneath, not to reduce confidence at the top.
