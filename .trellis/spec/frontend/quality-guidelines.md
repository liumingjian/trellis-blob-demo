# Quality Guidelines

> Code quality standards for frontend development.

---

## Overview

**Tooling:**
- ESLint + Prettier for code style
- TypeScript strict mode
- Husky pre-commit hooks

**Commands:**
```bash
npm run lint        # ESLint check
npm run typecheck   # TypeScript check
npm run format      # Prettier format
```

---

## Forbidden Patterns

| Pattern | Reason | Alternative |
|---------|--------|-------------|
| `any` type | Defeats TypeScript | Proper types or `unknown` |
| `// @ts-ignore` | Hides errors | Fix the type issue |
| `useEffect` for data fetching | Waterfalls | Server Components |
| Barrel exports (`index.ts`) | Bundle bloat | Direct imports |
| `console.log` in production | Noise | Remove or use logger |
| Inline styles | Hard to maintain | Tailwind classes |

---

## Required Patterns

| Pattern | When | Example |
|---------|------|---------|
| Explicit return types | Public functions | `function getName(): string` |
| Error boundaries | Page level | `error.tsx` in route |
| Loading states | Async operations | `loading.tsx` or Suspense |
| Form validation | All forms | Zod schemas |

---

## Testing Requirements

| Type | Coverage | Tool |
|------|----------|------|
| E2E | Critical user flows | agent-browser |
| Component | Complex interactions | Vitest + Testing Library |
| Unit | Utility functions | Vitest |

---

## Code Review Checklist

- [ ] No `any` types
- [ ] No `console.log`
- [ ] Error handling present
- [ ] Loading states handled
- [ ] Accessibility attributes
- [ ] TypeScript strict compliance
