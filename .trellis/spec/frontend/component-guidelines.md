# Component Guidelines

> React component patterns with shadcn/ui and Tailwind CSS.

---

## Overview

This project uses React Server Components (RSC) by default with shadcn/ui for UI primitives. Components follow a composition-first approach with explicit prop variants.

**Key Principles:**
- Server Components by default, Client Components only when needed
- Composition over configuration (avoid boolean prop proliferation)
- shadcn/ui as base, extend with project-specific variants

---

## Component Structure

```typescript
// components/articles/article-card.tsx
import { cn } from "@/lib/utils"
import { Card, CardContent, CardHeader } from "@/components/ui/card"
import type { Article } from "@/types"

interface ArticleCardProps {
  article: Article
  variant?: "default" | "compact"
  className?: string
}

export function ArticleCard({
  article,
  variant = "default",
  className
}: ArticleCardProps) {
  return (
    <Card className={cn("hover:shadow-md transition-shadow", className)}>
      <CardHeader>
        <h3>{article.title}</h3>
      </CardHeader>
      {variant === "default" && (
        <CardContent>
          <p>{article.excerpt}</p>
        </CardContent>
      )}
    </Card>
  )
}
```

---

## Props Conventions

**Use explicit variants instead of boolean props:**

```typescript
// Bad - boolean prop proliferation
interface ButtonProps {
  isLarge?: boolean
  isSmall?: boolean
  isPrimary?: boolean
  isOutline?: boolean
}

// Good - explicit variants
interface ButtonProps {
  size?: "sm" | "md" | "lg"
  variant?: "default" | "outline" | "ghost"
}
```

**Extend HTML element props:**

```typescript
interface InputProps extends React.InputHTMLAttributes<HTMLInputElement> {
  label?: string
  error?: string
}
```

---

## Styling Patterns

**Use Tailwind CSS with cn() utility:**

```typescript
import { cn } from "@/lib/utils"

// Merge conditional classes
<div className={cn(
  "base-styles",
  isActive && "active-styles",
  className
)} />
```

**shadcn/ui customization:**

```typescript
// Extend in components/ui/button.tsx
const buttonVariants = cva("base-classes", {
  variants: {
    variant: {
      default: "bg-primary text-primary-foreground",
      destructive: "bg-destructive text-destructive-foreground",
    },
    size: {
      sm: "h-8 px-3 text-xs",
      md: "h-10 px-4",
      lg: "h-12 px-6 text-lg",
    },
  },
  defaultVariants: {
    variant: "default",
    size: "md",
  },
})
```

---

## Accessibility

**Required for all interactive elements:**

```typescript
// Buttons must have accessible names
<Button aria-label="Close dialog">
  <XIcon />
</Button>

// Form inputs must have labels
<Label htmlFor="email">Email</Label>
<Input id="email" type="email" />

// Images must have alt text
<Image src={src} alt="Article featured image" />
```

**Keyboard navigation:**
- All interactive elements must be focusable
- Use `tabIndex={0}` only when necessary
- Implement `onKeyDown` for custom interactions

---

## Common Mistakes

| Mistake | Why It's Bad | Correct Approach |
|---------|--------------|------------------|
| `"use client"` everywhere | Breaks RSC benefits | Only add when using hooks/events |
| Inline objects in props | Causes re-renders | Hoist or memoize |
| Boolean prop proliferation | Hard to maintain | Use explicit variants |
| Missing `key` in lists | React reconciliation issues | Use stable unique IDs |
| Fetching in Client Components | Waterfalls, no caching | Fetch in Server Components |
