# Frontend Directory Structure

> Next.js 14+ App Router project organization for the Blog Application.

---

## Overview

This project uses Next.js App Router with a feature-based directory structure. All frontend code lives under `src/` with clear separation between app routes, components, and utilities.

---

## Directory Layout

```
src/
├── app/                      # Next.js App Router
│   ├── (auth)/               # Auth route group
│   │   ├── login/page.tsx
│   │   ├── register/page.tsx
│   │   └── forgot-password/page.tsx
│   ├── (public)/             # Public pages
│   │   ├── page.tsx          # Home (article list)
│   │   └── articles/[slug]/page.tsx
│   ├── dashboard/            # Protected admin area
│   │   ├── layout.tsx
│   │   ├── page.tsx
│   │   └── articles/
│   │       ├── page.tsx
│   │       ├── new/page.tsx
│   │       └── [id]/edit/page.tsx
│   ├── api/auth/[...nextauth]/route.ts
│   ├── layout.tsx
│   ├── loading.tsx
│   ├── error.tsx
│   └── not-found.tsx
├── components/
│   ├── ui/                   # shadcn/ui components
│   ├── layout/               # Header, Footer, Sidebar
│   ├── articles/             # Article components
│   └── auth/                 # Auth forms
├── lib/
│   ├── auth.ts               # NextAuth config
│   ├── prisma.ts             # Prisma client
│   ├── utils.ts              # Utilities (cn, etc.)
│   └── validations/          # Zod schemas
├── hooks/                    # Custom hooks
├── types/                    # TypeScript types
└── styles/globals.css
```

---

## Module Organization

### Route Groups

Use `(groupName)` to organize routes without affecting URLs:

```
app/
├── (auth)/      # /login, /register
├── (public)/    # /, /articles/[slug]
└── dashboard/   # /dashboard/*
```

### Co-location

- **Page-specific**: `_components/`, `_hooks/` next to page
- **Shared**: `src/components/`, `src/hooks/`

---

## Naming Conventions

| Type | Convention | Example |
|------|------------|---------|
| Directories | kebab-case | `article-editor/` |
| Components | kebab-case file, PascalCase export | `article-card.tsx` → `ArticleCard` |
| Hooks | use prefix | `use-auth.ts` → `useAuth` |
| Types | PascalCase | `Article`, `User` |

---

## Import Aliases

```json
{
  "paths": {
    "@/*": ["./src/*"],
    "@/components/*": ["./src/components/*"],
    "@/lib/*": ["./src/lib/*"]
  }
}
```

```typescript
// Good
import { Button } from "@/components/ui/button"

// Bad
import { Button } from "../../../components/ui/button"
```

---

## Forbidden Patterns

| Pattern | Reason | Alternative |
|---------|--------|-------------|
| PascalCase files | Inconsistent | kebab-case |
| Deep nesting (>3) | Hard to navigate | Route groups |
| Barrel exports | Bundle bloat | Direct imports |
| Mixed pages/app | Conflicts | app/ only |
