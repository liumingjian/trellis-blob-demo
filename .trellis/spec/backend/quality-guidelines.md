# Quality Guidelines

> Code quality standards for backend development.

---

## Overview

- TypeScript strict mode
- Zod for input validation
- Prisma for type-safe queries
- Server Actions for mutations

---

## Forbidden Patterns

| Pattern | Reason | Alternative |
|---------|--------|-------------|
| Raw SQL | Injection risk | Prisma queries |
| `any` type | No safety | Proper types |
| Unvalidated input | Security | Zod validation |

---

## Required Patterns

| Pattern | When | Example |
|---------|------|---------|
| Input validation | All inputs | Zod schemas |
| Auth check | Protected routes | `getServerSession()` |
| Error handling | All operations | try-catch |

---

## Testing Requirements

| Type | Coverage | Tool |
|------|----------|------|
| E2E | Auth flows | agent-browser |
| Integration | API routes | Vitest |

---

## Code Review Checklist

- [ ] Input validated with Zod
- [ ] Auth check on protected routes
- [ ] Error handling present
- [ ] No raw SQL queries
