# Directory Structure

> Backend code organization with Next.js App Router.

---

## Overview

Backend code is co-located with frontend in Next.js App Router structure:
- **API Routes**: `src/app/api/`
- **Server Actions**: `src/app/actions/`
- **Database**: `prisma/` at project root

---

## Directory Layout

```
prisma/
├── schema.prisma     # Database schema
└── migrations/       # Migration files

src/
├── app/
│   ├── api/          # REST API routes
│   │   └── auth/[...nextauth]/route.ts
│   └── actions/      # Server Actions
│       ├── articles.ts
│       └── auth.ts
├── lib/
│   ├── prisma.ts     # Prisma client singleton
│   ├── auth.ts       # NextAuth config
│   └── validations/  # Zod schemas
└── types/            # Shared types
```

---

## Module Organization

| Type | Location | Purpose |
|------|----------|---------|
| API Routes | `app/api/` | External REST endpoints |
| Server Actions | `app/actions/` | Form mutations |
| Business Logic | `lib/services/` | Reusable logic |
| Database | `lib/prisma.ts` | Prisma client |

---

## Naming Conventions

| Type | Convention | Example |
|------|------------|---------|
| API routes | `route.ts` | `api/articles/route.ts` |
| Server Actions | camelCase | `createArticle` |
| Services | PascalCase | `ArticleService` |

---

## Examples

```typescript
// app/actions/articles.ts
"use server"

import { prisma } from "@/lib/prisma"
import { articleSchema } from "@/lib/validations/article"

export async function createArticle(formData: FormData) {
  const data = articleSchema.parse(Object.fromEntries(formData))
  return prisma.article.create({ data })
}
```
