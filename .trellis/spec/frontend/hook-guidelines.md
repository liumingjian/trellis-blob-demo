# Hook Guidelines

> Custom hooks and data fetching patterns for the Blog Application.

---

## Overview

Prefer Server Components for data fetching. Use custom hooks only in Client Components for:
- Form state management
- Client-side interactions
- Browser APIs (localStorage, etc.)

**Key Principle:** Fetch data in Server Components, pass to Client Components as props.

---

## Custom Hook Patterns

```typescript
// hooks/use-auth.ts
"use client"

import { useSession } from "next-auth/react"

export function useAuth() {
  const { data: session, status } = useSession()

  return {
    user: session?.user,
    isLoading: status === "loading",
    isAuthenticated: status === "authenticated",
  }
}
```

```typescript
// hooks/use-form-state.ts
"use client"

import { useState } from "react"

export function useFormState<T>(initialState: T) {
  const [values, setValues] = useState(initialState)
  const [errors, setErrors] = useState<Partial<Record<keyof T, string>>>({})

  const setValue = (key: keyof T, value: T[keyof T]) => {
    setValues(prev => ({ ...prev, [key]: value }))
    setErrors(prev => ({ ...prev, [key]: undefined }))
  }

  return { values, errors, setValue, setErrors }
}
```

---

## Data Fetching

**Server Components (preferred):**

```typescript
// app/dashboard/articles/page.tsx
import { prisma } from "@/lib/prisma"

export default async function ArticlesPage() {
  const articles = await prisma.article.findMany()
  return <ArticleList articles={articles} />
}
```

**Client Components (when needed):**

```typescript
// Use Server Actions for mutations
"use client"

import { useTransition } from "react"
import { createArticle } from "@/app/actions/articles"

export function CreateArticleForm() {
  const [isPending, startTransition] = useTransition()

  const handleSubmit = (formData: FormData) => {
    startTransition(() => createArticle(formData))
  }

  return <form action={handleSubmit}>...</form>
}
```

---

## Naming Conventions

| Pattern | Example | Purpose |
|---------|---------|---------|
| `use{Feature}` | `useAuth` | Feature-specific logic |
| `use{Action}` | `useFormState` | Reusable action patterns |
| `use{Resource}` | `useArticles` | Resource management |

---

## Common Mistakes

| Mistake | Why It's Bad | Correct Approach |
|---------|--------------|------------------|
| Fetching in useEffect | Waterfalls, no SSR | Server Components |
| Missing dependency array | Infinite loops | Include all deps |
| Object/array in deps | Always re-runs | Use primitives or useMemo |
| Calling hooks conditionally | Breaks React rules | Always call at top level |
