# Type Safety

> TypeScript patterns and runtime validation.

---

## Overview

- **TypeScript strict mode** enabled
- **Zod** for runtime validation
- **Prisma** generates database types
- Infer types from Zod schemas when possible

---

## Type Organization

```
src/types/
├── index.ts      # Re-export all types
└── api.ts        # API response types

src/lib/validations/
├── auth.ts       # Auth schemas
└── article.ts    # Article schemas
```

---

## Validation

```typescript
// lib/validations/article.ts
import { z } from "zod"

export const articleSchema = z.object({
  title: z.string().min(1).max(200),
  content: z.string().min(1),
  status: z.enum(["DRAFT", "PUBLISHED"]),
})

export type ArticleInput = z.infer<typeof articleSchema>
```

---

## Common Patterns

```typescript
// Infer from Prisma
import type { Article } from "@prisma/client"

// Type guard
function isArticle(obj: unknown): obj is Article {
  return typeof obj === "object" && obj !== null && "id" in obj
}
```

---

## Forbidden Patterns

| Pattern | Reason | Alternative |
|---------|--------|-------------|
| `any` | No type safety | `unknown` + type guard |
| `as Type` assertions | Bypasses checks | Proper typing |
| `// @ts-ignore` | Hides errors | Fix the issue |
| `!` non-null assertion | Runtime errors | Optional chaining |
