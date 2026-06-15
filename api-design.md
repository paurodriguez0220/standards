## Purpose

REST API design standards.

---

## URL Design

- Use nouns, not verbs: `/users` not `/getUsers`
- Plural for collections: `/users`, `/orders`
- Nested resources for ownership: `/users/{id}/orders`
- Lowercase, hyphen-separated: `/user-profiles` not `/userProfiles`

---

## HTTP Methods

| Method | Use |
| --- | --- |
| `GET` | Read — never mutate state |
| `POST` | Create a new resource |
| `PUT` | Replace a resource entirely |
| `PATCH` | Partial update |
| `DELETE` | Remove a resource |

---

## Status Codes

Use the right code — don't return `200` for everything.

| Code | Meaning |
| --- | --- |
| `200 OK` | Success with body |
| `201 Created` | Resource created (POST) |
| `204 No Content` | Success, no body |
| `400 Bad Request` | Client sent invalid data |
| `401 Unauthorized` | Not authenticated |
| `403 Forbidden` | Authenticated but not allowed |
| `404 Not Found` | Resource doesn't exist |
| `409 Conflict` | State conflict (duplicate, version mismatch) |
| `422 Unprocessable` | Valid syntax, invalid semantics |
| `500 Internal Server Error` | Something broke on the server |

---

## Request & Response

- JSON everywhere. `Content-Type: application/json`.
- Use camelCase for JSON field names.
- Never expose internal database IDs as the only identifier — consider UUIDs for public APIs.
- Always return a consistent error shape:

```json
{
  "error": {
    "code": "VALIDATION_FAILED",
    "message": "Email is required.",
    "details": []
  }
}
```

---

## Versioning

Version in the URL path: `/api/v1/users`

- Introduce a new version for breaking changes only.
- Support the previous version for a migration window.
- Document what changed between versions.

---

## TODO

> _Add pagination standards, auth patterns, and rate limiting details here._
