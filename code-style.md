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

## ORM / Entity Framework (Code-First)

Always use code-first migrations. The codebase is the source of truth for the schema — never modify the database directly.

### Models

- One class per file, named after the entity: `Order.cs`, `UserProfile.cs`
- Use data annotations or Fluent API — pick one per project and stay consistent. Prefer Fluent API for complex mappings; keep models clean.
- Explicit column types over convention defaults where precision matters (`decimal(18,2)`, `nvarchar(256)`).
- Always configure string lengths — don't rely on `nvarchar(max)` by default.

```csharp
// Fluent API — preferred for anything beyond simple mappings
entity.Property(e => e.Price)
      .HasColumnType("decimal(18,2)")
      .IsRequired();

entity.Property(e => e.Email)
      .HasMaxLength(256)
      .IsRequired();
```

### Migrations

- One migration per logical change. Don't batch unrelated schema changes into one migration.
- Migration names describe the change: `AddOrderStatusColumn`, `CreateUserProfileTable`.
- Never edit an applied migration. Add a new one.
- Review the generated migration before applying — EF doesn't always infer intent correctly.
- Migrations run automatically on deploy in non-production. Production migrations are deliberate and reviewed.

### Relationships

- Always define both sides of a relationship explicitly.
- Use navigation properties — don't load related data with raw IDs when the ORM can do it cleanly.
- Be explicit about cascade delete behaviour. Don't rely on convention defaults for anything that could cause data loss.

### Querying

- Never call `.ToList()` or `.ToArray()` before filtering — filter first, materialise last.
- No lazy loading — use explicit `.Include()` for related data. Lazy loading hides N+1 problems.
- Keep queries close to the repository. Business logic doesn't build LINQ expressions.

```csharp
// Good — filter in the query
var pending = await _db.Orders
    .Where(o => o.Status == OrderStatus.Pending)
    .Include(o => o.Items)
    .ToListAsync();

// Bad — loads everything then filters in memory
var pending = (await _db.Orders.ToListAsync())
    .Where(o => o.Status == OrderStatus.Pending);
```

---

## Language-Specific

> _Add language-specific conventions here as needed (e.g. .NET, TypeScript, Python)._

---

## Related

- [API Design](api-design.md)
- [Testing](testing.md)
