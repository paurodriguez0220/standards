## Purpose

Testing philosophy and standards.

---

## Philosophy

- Tests are first-class code. They deserve the same care as production code.
- A test that never fails is not a test — it's a false guarantee.
- Test behaviour, not implementation. Tests should survive refactors.
- Aim for fast feedback. Slow tests don't get run.

---

## Test Types

| Type | What it tests | Speed |
| --- | --- | --- |
| Unit | A single function or class in isolation | Fast |
| Integration | Multiple components working together | Medium |
| E2E | Full flows from the user's perspective | Slow |

Write more unit tests than integration tests. Write more integration tests than E2E.

---

## What to Test

- Happy path — the expected use case
- Edge cases — empty input, nulls, boundaries
- Error paths — what happens when things go wrong
- Regression cases — add a test every time you fix a bug

---

## What Not to Test

- Framework code you didn't write
- Trivial getters/setters with no logic
- Private implementation details

---

## Naming

Test names should describe: _what_ is being tested, _under what condition_, and _what the expected outcome is_.

```
// Good
calculateTotal_whenDiscountApplied_returnsReducedPrice()

// Bad
test1()
testCalculate()
```

---

## TODO

> _Add project-specific tooling, coverage thresholds, and CI integration details here._
