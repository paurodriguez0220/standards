## Purpose

How I manage branches, write commits, and run pull requests.

---

## Branching

Short-lived feature branches off `main`. No long-lived branches unless there's a clear reason.

### Branch naming

```
<type>/<short-description>
```

Types:
- `feat/` — new feature
- `fix/` — bug fix
- `chore/` — maintenance, deps, tooling
- `docs/` — documentation changes
- `refactor/` — structural improvement, no behaviour change

Examples:
```
feat/add-user-auth
fix/login-redirect-loop
chore/bump-dependencies
docs/update-api-readme
```

One branch per task. Don't mix unrelated changes in a single branch.

---

## Commits

Follow [Conventional Commits](https://www.conventionalcommits.org/).

### Format

```
<type>(<scope>): <short description>

[optional body]

[optional footer]
```

Types:
- `feat` — new feature
- `fix` — bug fix
- `chore` — maintenance
- `docs` — documentation only
- `refactor` — restructure, no behaviour change
- `test` — adding or fixing tests
- `ci` — CI/CD config changes
- `perf` — performance improvement

### Rules

- Present tense, imperative: "add feature" not "added feature" or "adds feature"
- Subject line under 72 characters
- Reference issues in footer: `Closes #123`
- Never vague: "fix stuff", "WIP", "updates" are not commits

### Examples

```
feat(auth): add JWT refresh token rotation

fix(api): return 404 when resource not found instead of 500

chore: upgrade dependencies to latest minor versions

docs(readme): add local dev setup instructions
```

---

## Pull Requests

### Size

- Small and focused. One feature or fix per PR.
- If a PR touches more than ~10 files, question whether it should be split.
- Large refactors are valid exceptions — explain why in the description.

### Description

Every PR needs:
1. **What** — what changed (one sentence)
2. **Why** — why the change was needed
3. **How to test** — what to check to verify it works

Don't auto-generate a description and merge. Write one sentence that makes the reviewer's job easier.

### Code review

- Approve only if you'd be comfortable owning the change yourself
- Comments should explain *why*, not just *what*
- Prefix nit-level feedback with `nit:` so the author can deprioritise
- Never merge your own PR without at least one review on shared codebases
- Resolve all open threads before merging

### Merge strategy

- **Squash merge** for feature branches — keeps `main` history readable
- **Merge commit** for release branches or long-lived integrations only
- Never force-push to `main`

---

## Main Branch Rules

- `main` is always deployable
- CI must be green before merging
- No direct commits to `main` — use PRs
- Branch protection enabled on all production repositories

---

## Tags & Releases

Use semantic versioning: `v{major}.{minor}.{patch}`

- **Patch** — backwards-compatible bug fix
- **Minor** — new backwards-compatible feature
- **Major** — breaking change

Tag on `main` after merge. Automate release notes where possible.
