# UI/UX Design Guidelines

> Design system and visual guidelines for the Blog Application.

---

## Overview

This design system establishes a cohesive visual language for the Blog Application, ensuring consistency across all user interfaces while maintaining flexibility for future growth.

### Design Philosophy

Our design approach is built on three core pillars:

1. **Clarity First** - Every design decision prioritizes user comprehension. Content is king in a blog application, and the UI should enhance readability, not compete with it.

2. **Purposeful Minimalism** - We embrace simplicity not as a limitation, but as a deliberate choice. Each element earns its place by serving a clear function.

3. **Accessible by Default** - Accessibility is not an afterthought. We design for all users from the start, ensuring WCAG 2.1 AA compliance as a baseline.

### Design Sources

Based on:
- **ui-ux-pro-max** - Design intelligence with 50+ styles, 97 color palettes, 57 font pairings
- **frontend-design** - Creative design principles and modern UI patterns

---

## Guidelines Index

| Guide | Description | Key Topics |
|-------|-------------|------------|
| [Design System](./design-system.md) | Core design tokens | Colors, typography, spacing, shadows, borders |
| [Style Guidelines](./style-guidelines.md) | Visual style patterns | Component styling, layout patterns, visual hierarchy |
| [Accessibility](./accessibility.md) | A11y requirements | WCAG compliance, keyboard nav, screen readers |
| [Interaction](./interaction-guidelines.md) | Hover, animation, feedback | Transitions, micro-interactions, loading states |

---

## Quick Reference

### Tech Stack

| Technology | Purpose | Version |
|------------|---------|---------|
| Next.js | React framework | 14+ (App Router) |
| Tailwind CSS | Utility-first CSS | 3.x |
| shadcn/ui | Component library | Latest |
| TypeScript | Type safety | 5.x |

### Key Design Principles

| Principle | Description | Implementation |
|-----------|-------------|----------------|
| Content Focus | UI supports content, not distracts | Generous whitespace, readable typography |
| Consistency | Predictable patterns | Reusable components, design tokens |
| Responsiveness | Works on all devices | Mobile-first approach, fluid layouts |
| Performance | Fast visual feedback | Optimized assets, skeleton loaders |
| Accessibility | Inclusive design | Semantic HTML, ARIA labels, contrast ratios |

### Color Quick Reference

```
Primary:     hsl(222.2, 47.4%, 11.2%)  - Brand color, CTAs
Secondary:   hsl(210, 40%, 96.1%)      - Backgrounds, accents
Destructive: hsl(0, 84.2%, 60.2%)      - Errors, warnings
Success:     hsl(142, 76%, 36%)        - Confirmations
```

### Typography Quick Reference

```
Headings:  font-sans (Geist Sans) - Bold, clear hierarchy
Body:      font-sans (Geist Sans) - Readable, comfortable
Code:      font-mono (Geist Mono) - Technical content
```

### Spacing Quick Reference

```
Tight:   4px  (space-1)  - Inline elements
Default: 16px (space-4)  - Standard gaps
Loose:   32px (space-8)  - Section separation
```

---

## Usage Guidelines

### When to Reference Each Document

- **Starting a new component?** Read [Design System](./design-system.md) for tokens
- **Styling decisions?** Check [Style Guidelines](./style-guidelines.md)
- **Adding interactions?** See [Interaction Guidelines](./interaction-guidelines.md)
- **Accessibility review?** Consult [Accessibility](./accessibility.md)

### Integration with shadcn/ui

All design tokens are configured to work seamlessly with shadcn/ui's theming system. Use CSS variables defined in `globals.css` and reference Tailwind classes that map to these tokens.
