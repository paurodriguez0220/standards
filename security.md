## Purpose

Security fundamentals that apply to every project.

---

## Secrets

- Never commit secrets to source control. Not even temporarily.
- Use environment variables or a secrets manager (Key Vault, AWS Secrets Manager, etc.).
- Rotate secrets when anyone with access leaves the team.
- Treat `.env` files as secrets — gitignore them always.

---

## Authentication & Authorisation

- Use established auth libraries — don't roll your own.
- Prefer short-lived tokens (JWTs with expiry) over long-lived sessions.
- Always authorise at the resource level, not just the route level.
- Validate on the server — client-side checks are UX, not security.

---

## Input Validation

- Never trust user input. Validate and sanitise at every system boundary.
- Parameterise all database queries — never concatenate user input into SQL.
- Encode output to prevent XSS.
- Validate file uploads: type, size, and content.

---

## Dependencies

- Keep dependencies updated. Unpatched packages are the most common attack vector.
- Run `npm audit` / `dotnet list package --vulnerable` / equivalent regularly.
- Remove unused dependencies.

---

## Logging

- Never log secrets, passwords, tokens, or PII.
- Log enough to reconstruct what happened — not so much you create a data liability.

---

## TODO

> _Add project-specific threat model, pen test findings, and compliance requirements here._
