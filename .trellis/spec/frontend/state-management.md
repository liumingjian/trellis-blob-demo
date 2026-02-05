# State Management

> State management patterns for the Blog Application.

---

## Overview

This project uses a minimal state approach:
- **Server State**: Managed by Server Components + Server Actions
- **Local State**: React useState for component-specific state
- **URL State**: Next.js searchParams for filters/pagination
- **No global state library** - avoid Redux/Zustand unless absolutely necessary

---

## State Categories

| Type | Solution | Example |
|------|----------|---------|
| Server State | Server Components | Article list, user data |
| Form State | useState | Input values, validation |
| UI State | useState | Modal open, dropdown |
| URL State | searchParams | Filters, pagination |

---

## When to Use Global State

**Rarely needed.** Consider global state only when:
- State is needed by many unrelated components
- Prop drilling exceeds 3 levels
- State must persist across route changes

**Prefer alternatives:**
- URL params for shareable state
- Server Components for data
- Context for theme/auth (already provided)

---

## Server State

```typescript
// Server Component fetches data
async function ArticlesPage() {
  const articles = await prisma.article.findMany()
  return <ArticleList articles={articles} />
}

// Mutations via Server Actions
"use server"
export async function updateArticle(id: string, data: FormData) {
  await prisma.article.update({ where: { id }, data })
  revalidatePath("/dashboard/articles")
}
```

---

## Common Mistakes

| Mistake | Why It's Bad | Correct Approach |
|---------|--------------|------------------|
| Global state for server data | Stale data, complexity | Server Components |
| useState for URL state | Not shareable/bookmarkable | searchParams |
| Derived state in useState | Out of sync | Compute during render |
| Over-using Context | Re-renders entire tree | Keep state local |
