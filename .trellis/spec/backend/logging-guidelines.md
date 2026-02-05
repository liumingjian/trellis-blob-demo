# Logging Guidelines

> Structured logging patterns for the Blog Application.

---

## Overview

- Use `console` for development
- Structured JSON for production
- Never log sensitive data

---

## Log Levels

| Level | When to Use |
|-------|-------------|
| error | Failures requiring attention |
| warn | Unexpected but handled |
| info | Key business events |
| debug | Development only |

---

## Structured Logging

```typescript
console.log(JSON.stringify({
  level: "info",
  message: "Article created",
  articleId: article.id,
  userId: session.user.id,
  timestamp: new Date().toISOString()
}))
```

---

## What to Log

- Authentication events
- Article CRUD operations
- Errors with context

---

## What NOT to Log

- Passwords
- Session tokens
- Email addresses
- Full request bodies
