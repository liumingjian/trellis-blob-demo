# Error Handling

> Error handling patterns for the Blog Application.

---

## Overview

- Use custom error classes for domain errors
- Return consistent JSON error responses
- Log errors with context
- Never expose internal errors to clients

---

## Error Types

```typescript
// lib/errors.ts
export class AppError extends Error {
  constructor(
    message: string,
    public code: string,
    public statusCode: number = 400
  ) {
    super(message)
  }
}

export class NotFoundError extends AppError {
  constructor(resource: string) {
    super(`${resource} not found`, "NOT_FOUND", 404)
  }
}
```

---

## Error Handling Patterns

```typescript
// Server Action pattern
export async function getArticle(id: string) {
  const article = await prisma.article.findUnique({ where: { id } })
  if (!article) throw new NotFoundError("Article")
  return article
}
```

---

## API Error Responses

```typescript
// Standard format
{
  "error": {
    "code": "NOT_FOUND",
    "message": "Article not found"
  }
}
```

---

## Common Mistakes

| Mistake | Reason | Alternative |
|---------|--------|-------------|
| Exposing stack traces | Security risk | Generic message |
| Silent catch | Hides bugs | Log and rethrow |
| String errors | No structure | Custom error class |
