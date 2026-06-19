## Purpose

Standards for project documentation — what every project needs, how to structure it, and what belongs where.

---

## Every Project Needs a README

No exceptions. A project without a README is incomplete.

### Required sections

```markdown
# Project Name

One sentence: what this project is and who uses it.

## Getting Started
Prerequisites, how to clone, how to run locally.

## Commands
| Command | What it does |
| --- | --- |
| `dotnet run` | Start the API |
| `dotnet test` | Run all tests |
| `dotnet ef database update` | Apply pending migrations |

## Architecture
Key moving parts — main layers, external dependencies, notable patterns.
Keep it to a paragraph or a simple diagram. Not a novel.
Explicitly name the design patterns used (Options pattern, Strategy, Factory, Orchestrator, etc.).

## Dependencies
All external services, NuGet packages, and integrations the app needs at runtime.
| Dependency | Purpose |
| --- | --- |
| _external service or package_ | _what the app uses it for_ |

List only runtime dependencies — not build tools or test libraries.

## Configuration
Environment variables and secrets required to run — names, not values.

## Links
- Production URL
- Staging/test URL
- Related repos
- Standards: https://github.com/paurodriguez0220/standards-docs
```

### Rules

- Write the README for someone joining the project cold — they should be able to run it locally in under 10 minutes.
- Commands must be copy-pasteable and current. A README with broken setup steps is worse than none.
- Architecture must explicitly name design patterns — "Orchestrator pattern", "Strategy + Factory", not just "there are services".
- Dependencies section must list every runtime external service or significant NuGet package. If a dependency requires setup (API keys, accounts), link to or summarize the setup steps.
- No corporate fluff. No "this project leverages cutting-edge technology to deliver business value."
- Update the README when the setup changes. It's part of the work, not an afterthought.

---

## CLAUDE.md

Every project also needs a `CLAUDE.md` at the repo root for AI agent context. See [Working with AI Agents](ai-workflow.md) for the full template and rules.

---

## Docs Folder

Create a `docs/` folder when the project has content that doesn't belong in the README — design decisions, runbooks, integration guides.

```
docs/
├── architecture.md         ← system overview, diagrams
├── decisions/              ← ADRs (see below)
│   ├── 001-use-ef-core.md
│   └── 002-jwt-auth.md
├── issues/                 ← bugs / vendor limitations (see below)
│   ├── queue/              ← newly discovered, root cause not yet confirmed
│   ├── defined/            ← root cause known; won't fix or fix planned
│   └── finished/           ← resolved, kept for reference
├── runbooks/               ← operational procedures
│   └── rotate-secrets.md
└── tasks/                  ← lightweight task tracking (see below)
    ├── queue/              ← idea or rough plan, not yet designed
    ├── defined/            ← fully planned, ready to implement
    └── finished/           ← completed, kept for reference
```

Don't create `docs/` just to have it. One well-written README is better than a docs folder with three stale files.

---

## Issues

Create a `docs/issues/` folder to document bugs or limitations — anything reproducible that has been investigated or is worth tracking. Issues follow the same three-stage lifecycle as tasks.

```
docs/issues/
├── queue/      ← newly discovered; symptom described, root cause not yet confirmed
├── defined/    ← root cause known; decision made (won't fix, workaround, or fix planned)
└── finished/   ← resolved; kept as a record
```

One file per issue. Advance the file through the lifecycle: `queue/` → `defined/` → `finished/`. Never delete — move.

Name the file after the symptom, not the cause: `pdf-missing-letter.md`, not `pdfpig-nel-bug.md`.

### Lifecycle

| Folder | Meaning |
| --- | --- |
| `queue/` | Newly discovered. What happens is documented. Root cause is not yet confirmed. |
| `defined/` | Root cause identified. A decision has been made: won't fix, workaround documented, or a fix is planned. |
| `finished/` | Resolved. Moved here to preserve the investigation record. |

### Template — Queue (open issue)

```markdown
# Issue: <Short title — what the user sees>

**Status:** Open

## What Happens
<Concrete description. Include an example, table, or before/after if it helps.>

## Context
<What was already investigated. Possible causes.>

## Acceptance Criteria
- [ ] Root cause confirmed
- [ ] Decision made (fix, workaround, or won't fix)
```

### Template — Defined (root cause known)

```markdown
# Issue: <Short title>

**Status:** Will not fix (<reason>) | Fix planned | Workaround in place

## What Happens
<Concrete description.>

## Context
<Root cause explanation. Technical detail as needed.>

## Possible Workaround (not implemented)
<Optional. What would be needed to fix it upstream or in a future rewrite.>

## Acceptance Criteria
- [x] Root cause identified and documented
- [ ] <Any remaining actions>

---
*Added: YYYY-MM-DD*
```

### When to write one

- A bug is reproducible but the fix is upstream, impractical, or deferred.
- A behaviour looks wrong but is a library constraint — future maintainers will waste time investigating it again.
- Any newly discovered problem worth tracking before root cause is known.

Do not write issues for tasks that are fully planned — use `docs/tasks/` instead.

---

## Task Tracking in the Repo

For personal projects or projects without a ticket system, use `docs/tasks/` to track planned work.

```
docs/tasks/
├── queue/      ← idea or rough plan, not yet fully designed
├── defined/    ← fully planned with implementation steps, ready to start
└── finished/   ← done, kept for reference
```

One file per task. Advance the file through the lifecycle: `queue/` → `defined/` → `finished/`. Never delete — move.

### Lifecycle

| Folder | Meaning |
| --- | --- |
| `queue/` | The task has been identified. Goal and context are written. Design is rough or TBD. |
| `defined/` | The task has a detailed implementation plan. File changes, patterns, and acceptance criteria are clear. Ready to pick up and execute without further design work. |
| `finished/` | Done. Kept as a record of intent and decisions. |

### Template — Queue (lightweight)

```markdown
# Task: <Short title>

**Status:** Planned

## Goal
One sentence.

## Context
Why this matters. What triggered it.

## Proposed Design
Enough detail to capture the idea — not a full spec.

## Acceptance Criteria
- [ ] Item one
- [ ] Item two
```

### Template — Defined (full plan)

```markdown
# Task: <Short title>

**Status:** Defined

## Goal
One sentence.

## Context
Why this matters. What triggered it. Key constraints.

## Implementation Plan

### Step 1 — <name>
Which files change, what they do, and why.

### Step 2 — <name>
...

## Acceptance Criteria
- [ ] Item one
- [ ] Item two

---
*Added: YYYY-MM-DD | Updated: YYYY-MM-DD — <reason for last update>*
```

Use `docs/tasks/` when:
- The project has no issue tracker.
- The task is specific enough to need design notes before starting.
- You want a lightweight record of intent and decisions for future reference.

Don't use it as a substitute for a proper tracker on a shared team project.

---

## Architecture Decision Records (ADRs)

Write an ADR when you make a significant decision that future contributors will wonder about — why this library, why this pattern, why not the obvious alternative.

### Template

```markdown
# ADR-{number}: {Short title}

**Date:** YYYY-MM-DD
**Status:** Accepted | Superseded by ADR-{n}

## Context
What problem were we solving? What constraints existed?

## Decision
What did we decide to do?

## Consequences
What does this make easier? What does it make harder?
```

### When to write one

- Choosing a framework, library, or external service
- Deviating from the standards in this repo (and why)
- Significant architectural changes — new layer, new pattern, new integration
- Decisions you expect to be questioned in a future code review

### When not to write one

- Implementation details that are obvious from the code
- Decisions that can be reversed cheaply
- Anything already covered by the standards repo

---

## What Not to Document Here

| Belongs in | Not in docs |
| --- | --- |
| Code (names, types, structure) | "What does this function do?" |
| Git history / commit messages | "Why was this changed?" |
| This standards repo | Language conventions, patterns, workflow rules |
| Tickets / issues | Requirements, acceptance criteria |

Don't duplicate information across multiple places. Pick where something lives and link to it everywhere else.

---

## Signature

Every project README and doc file ends with a signature block:

```markdown
---
*Maintained by paurodriguez0220 · Last updated: YYYY-MM-DD*
*Standards: https://github.com/paurodriguez0220/standards-docs*
```

Update the date when the document changes. The signature is a signal that the document is actively owned, not abandoned.

---

## Related

- [Working with AI Agents](ai-workflow.md)
- [Git Workflow](git-workflow.md)

---
*Maintained by paurodriguez0220 · Last updated: 2026-06-19 · Issues folder now follows same queue/defined/finished lifecycle as tasks*
*Standards: https://github.com/paurodriguez0220/standards-docs*
