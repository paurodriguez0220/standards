## Purpose

How I work effectively with AI coding agents (Claude Code, Copilot, etc.).

---

## Mindset

- AI does the heavy lifting. You set the standard.
- Treat AI output as a first draft from a capable junior — review it like you own it.
- The AI doesn't know what it doesn't know. Provide context; don't assume it will ask.

---

## Prompting

- Give context upfront: what you're building, the constraint, the desired outcome.
- Specify the *why*, not just the *what* — agents make better decisions with motivation.
- Break large tasks into scoped steps. One clear goal per prompt.
- Reference specific files, functions, or line numbers when relevant.

---

## Review

- Always read the diff before accepting a change.
- Run tests. AI-generated code can be confidently wrong.
- Check for: security issues, hardcoded values, missing error handling, off-by-one logic.
- Don't merge anything you don't understand well enough to debug.

---

## What AI is Good For

- Boilerplate and scaffolding
- Writing and expanding tests
- Documentation and comments
- Refactoring to a pattern you've already defined
- Debugging with a full error + context paste
- Exploring unfamiliar APIs or frameworks

---

## What AI is Not Good For (Without Supervision)

- Architectural decisions — it will satisfy the prompt, not the system
- Security-sensitive code — verify every line
- Large untested rewrites
- Anything you wouldn't be able to explain to a colleague

---

## CLAUDE.md

Every project should have a `CLAUDE.md` at the repo root. It tells Claude Code:

- What the project is and how it's structured
- Build, test, and run commands
- Conventions to follow
- Things to never do

Keep `CLAUDE.md` updated. It's the agent's operating manual for the project.

---

## TODO

> _Add specific tooling config, MCP server usage, and agent permission settings here._
