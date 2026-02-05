# Database Guidelines

> Prisma ORM patterns for PostgreSQL.

---

## Overview

- **ORM**: Prisma
- **Database**: PostgreSQL
- **Schema**: `prisma/schema.prisma`
- **Client**: Singleton in `lib/prisma.ts`

---

## Query Patterns

```typescript
// lib/prisma.ts - Singleton
import { PrismaClient } from "@prisma/client"

const globalForPrisma = globalThis as { prisma?: PrismaClient }
export const prisma = globalForPrisma.prisma ?? new PrismaClient()
if (process.env.NODE_ENV !== "production") globalForPrisma.prisma = prisma
```

```typescript
// Select only needed fields
const articles = await prisma.article.findMany({
  select: { id: true, title: true, slug: true }
})
```

---

## Migrations

```bash
# Create migration
npx prisma migrate dev --name add_articles

# Apply in production
npx prisma migrate deploy

# Reset database (dev only)
npx prisma migrate reset
```

---

## Naming Conventions

| Type | Convention | Example |
|------|------------|---------|
| Models | PascalCase singular | `Article`, `User` |
| Fields | camelCase | `createdAt`, `authorId` |
| Relations | camelCase | `author`, `articles` |

---

## Common Mistakes

| Mistake | Reason | Alternative |
|---------|--------|-------------|
| N+1 queries | Performance | Use `include` |
| No select | Over-fetching | Select needed fields |
| Raw SQL | Injection risk | Prisma queries |
