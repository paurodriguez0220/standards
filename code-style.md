## Purpose

Coding conventions that apply across projects regardless of language.

---

## Naming

- Names should reveal intent. If a name needs a comment to explain it, rename it.
- Avoid abbreviations unless they're universally understood (`id`, `url`, `api`)
- Boolean names should read as questions: `isActive`, `hasPermission`, `canEdit`
- Functions should be verbs: `getUser`, `calculateTotal`, `sendEmail`
- Classes and types should be nouns: `UserService`, `OrderRepository`

---

## Functions & Methods

- One function, one responsibility. If you can't describe a function in one sentence, split it.
- Aim for under ~20 lines. More than that: consider splitting.
- Prefer fewer parameters. More than 3–4 is a smell — consider a config object.
- Avoid side effects where possible. Pure functions are easier to test and reason about.

---

## Files & Modules

- One primary concept per file.
- File name matches the primary class/function/module it contains.
- Group related files in folders by domain, not by type.

---

## General Rules

- No magic strings or numbers — use named constants.
- No commented-out code — that's what git history is for.
- No TODO comments without a linked issue.
- Fail fast and explicitly. Don't silently swallow errors.
- Prefer explicit over implicit — don't make the reader guess.

---

## Language-Specific

> _Add language-specific conventions here as needed (e.g. .NET, TypeScript, Python)._

---

## Related

- [API Design](api-design.md)
- [Testing](testing.md)
