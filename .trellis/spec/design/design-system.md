# Design System

> Core design tokens for the Blog Application - colors, typography, spacing, and more.

---

## Color Palette

All colors use HSL format compatible with shadcn/ui and Tailwind CSS. Define these in your `globals.css` within the `:root` selector.

### Primary Colors (Brand)

| Token | HSL Value | Tailwind Class | Usage |
|-------|-----------|----------------|-------|
| `--primary` | `222.2 47.4% 11.2%` | `bg-primary` | Primary buttons, links, brand elements |
| `--primary-foreground` | `210 40% 98%` | `text-primary-foreground` | Text on primary backgrounds |

```css
/* CSS Variables */
--primary: 222.2 47.4% 11.2%;
--primary-foreground: 210 40% 98%;
```

### Secondary Colors

| Token | HSL Value | Tailwind Class | Usage |
|-------|-----------|----------------|-------|
| `--secondary` | `210 40% 96.1%` | `bg-secondary` | Secondary buttons, subtle backgrounds |
| `--secondary-foreground` | `222.2 47.4% 11.2%` | `text-secondary-foreground` | Text on secondary backgrounds |

```css
--secondary: 210 40% 96.1%;
--secondary-foreground: 222.2 47.4% 11.2%;
```

### Neutral / Gray Scale

| Token | HSL Value | Tailwind Class | Usage |
|-------|-----------|----------------|-------|
| `--background` | `0 0% 100%` | `bg-background` | Page backgrounds |
| `--foreground` | `222.2 84% 4.9%` | `text-foreground` | Primary text |
| `--muted` | `210 40% 96.1%` | `bg-muted` | Muted backgrounds, disabled states |
| `--muted-foreground` | `215.4 16.3% 46.9%` | `text-muted-foreground` | Secondary text, placeholders |
| `--accent` | `210 40% 96.1%` | `bg-accent` | Hover states, highlights |
| `--accent-foreground` | `222.2 47.4% 11.2%` | `text-accent-foreground` | Text on accent backgrounds |

```css
--background: 0 0% 100%;
--foreground: 222.2 84% 4.9%;
--muted: 210 40% 96.1%;
--muted-foreground: 215.4 16.3% 46.9%;
--accent: 210 40% 96.1%;
--accent-foreground: 222.2 47.4% 11.2%;
```

### Semantic Colors

| Token | HSL Value | Tailwind Class | Usage |
|-------|-----------|----------------|-------|
| `--destructive` | `0 84.2% 60.2%` | `bg-destructive` | Error states, delete actions |
| `--destructive-foreground` | `210 40% 98%` | `text-destructive-foreground` | Text on destructive backgrounds |
| `--success` | `142 76% 36%` | Custom | Success messages, confirmations |
| `--warning` | `38 92% 50%` | Custom | Warning messages, cautions |
| `--info` | `199 89% 48%` | Custom | Informational messages |

```css
--destructive: 0 84.2% 60.2%;
--destructive-foreground: 210 40% 98%;

/* Extended semantic colors (add to globals.css) */
--success: 142 76% 36%;
--success-foreground: 210 40% 98%;
--warning: 38 92% 50%;
--warning-foreground: 222.2 84% 4.9%;
--info: 199 89% 48%;
--info-foreground: 210 40% 98%;
```

### UI Element Colors

```css
--card: 0 0% 100%;
--card-foreground: 222.2 84% 4.9%;
--popover: 0 0% 100%;
--popover-foreground: 222.2 84% 4.9%;
--border: 214.3 31.8% 91.4%;
--input: 214.3 31.8% 91.4%;
--ring: 222.2 84% 4.9%;
```

---

## Typography

### Font Families

| Font | Variable | Usage | Fallback Stack |
|------|----------|-------|----------------|
| Geist Sans | `font-sans` | Headings, body text | `ui-sans-serif, system-ui, sans-serif` |
| Geist Mono | `font-mono` | Code blocks, technical | `ui-monospace, monospace` |

```css
/* Tailwind config */
fontFamily: {
  sans: ['var(--font-geist-sans)', 'ui-sans-serif', 'system-ui', 'sans-serif'],
  mono: ['var(--font-geist-mono)', 'ui-monospace', 'monospace'],
}
```

### Font Size Scale

| Name | Size | Tailwind | Line Height | Usage |
|------|------|----------|-------------|-------|
| xs | 0.75rem (12px) | `text-xs` | 1rem | Captions, labels |
| sm | 0.875rem (14px) | `text-sm` | 1.25rem | Secondary text, metadata |
| base | 1rem (16px) | `text-base` | 1.5rem | Body text |
| lg | 1.125rem (18px) | `text-lg` | 1.75rem | Lead paragraphs |
| xl | 1.25rem (20px) | `text-xl` | 1.75rem | Small headings |
| 2xl | 1.5rem (24px) | `text-2xl` | 2rem | H4 headings |
| 3xl | 1.875rem (30px) | `text-3xl` | 2.25rem | H3 headings |
| 4xl | 2.25rem (36px) | `text-4xl` | 2.5rem | H2 headings |
| 5xl | 3rem (48px) | `text-5xl` | 1 | H1 headings |

### Font Weights

| Name | Weight | Tailwind | Usage |
|------|--------|----------|-------|
| Normal | 400 | `font-normal` | Body text |
| Medium | 500 | `font-medium` | Emphasis, labels |
| Semibold | 600 | `font-semibold` | Subheadings, buttons |
| Bold | 700 | `font-bold` | Headings, strong emphasis |

### Heading Styles

| Element | Size | Weight | Letter Spacing | Tailwind Classes |
|---------|------|--------|----------------|------------------|
| h1 | 2.25rem | 700 | -0.025em | `text-4xl font-bold tracking-tight` |
| h2 | 1.875rem | 600 | -0.025em | `text-3xl font-semibold tracking-tight` |
| h3 | 1.5rem | 600 | normal | `text-2xl font-semibold` |
| h4 | 1.25rem | 600 | normal | `text-xl font-semibold` |
| h5 | 1.125rem | 500 | normal | `text-lg font-medium` |
| h6 | 1rem | 500 | normal | `text-base font-medium` |

### Line Heights

| Name | Value | Tailwind | Usage |
|------|-------|----------|-------|
| None | 1 | `leading-none` | Large headings |
| Tight | 1.25 | `leading-tight` | Headings |
| Snug | 1.375 | `leading-snug` | Subheadings |
| Normal | 1.5 | `leading-normal` | Body text |
| Relaxed | 1.625 | `leading-relaxed` | Long-form content |
| Loose | 2 | `leading-loose` | Spacious text |

---

## Spacing

### Tailwind Spacing Scale

| Name | Value | Tailwind | Usage |
|------|-------|----------|-------|
| 0 | 0px | `p-0`, `m-0` | Reset spacing |
| px | 1px | `p-px`, `m-px` | Hairline borders |
| 0.5 | 2px | `p-0.5`, `m-0.5` | Micro spacing |
| 1 | 4px | `p-1`, `m-1` | Tight inline spacing |
| 1.5 | 6px | `p-1.5`, `m-1.5` | Small gaps |
| 2 | 8px | `p-2`, `m-2` | Compact spacing |
| 3 | 12px | `p-3`, `m-3` | Default small |
| 4 | 16px | `p-4`, `m-4` | Default medium |
| 5 | 20px | `p-5`, `m-5` | Comfortable |
| 6 | 24px | `p-6`, `m-6` | Generous |
| 8 | 32px | `p-8`, `m-8` | Section gaps |
| 10 | 40px | `p-10`, `m-10` | Large sections |
| 12 | 48px | `p-12`, `m-12` | Page sections |
| 16 | 64px | `p-16`, `m-16` | Major sections |

### Common Spacing Patterns

| Pattern | Spacing | Tailwind | Example |
|---------|---------|----------|---------|
| Inline elements | 4-8px | `gap-1`, `gap-2` | Icon + text |
| Form fields | 8-12px | `space-y-2`, `space-y-3` | Label + input |
| Card padding | 16-24px | `p-4`, `p-6` | Card content |
| Section gap | 32-48px | `py-8`, `py-12` | Between sections |
| Page padding | 16-32px | `px-4`, `px-8` | Container edges |

### Gap Utilities

```tsx
// Flex/Grid gaps
<div className="flex gap-2">     {/* 8px gap */}
<div className="flex gap-4">     {/* 16px gap */}
<div className="grid gap-6">     {/* 24px gap */}

// Stack spacing
<div className="space-y-4">      {/* 16px vertical */}
<div className="space-x-2">      {/* 8px horizontal */}
```

---

## Shadows

### Shadow Scale

| Name | Value | Tailwind | Usage |
|------|-------|----------|-------|
| sm | `0 1px 2px rgba(0,0,0,0.05)` | `shadow-sm` | Subtle elevation |
| default | `0 1px 3px rgba(0,0,0,0.1), 0 1px 2px rgba(0,0,0,0.06)` | `shadow` | Cards, buttons |
| md | `0 4px 6px rgba(0,0,0,0.1), 0 2px 4px rgba(0,0,0,0.06)` | `shadow-md` | Dropdowns, popovers |
| lg | `0 10px 15px rgba(0,0,0,0.1), 0 4px 6px rgba(0,0,0,0.05)` | `shadow-lg` | Modals, dialogs |
| xl | `0 20px 25px rgba(0,0,0,0.1), 0 10px 10px rgba(0,0,0,0.04)` | `shadow-xl` | Large overlays |
| none | `none` | `shadow-none` | Remove shadow |

### CSS Variables

```css
--shadow-sm: 0 1px 2px rgba(0,0,0,0.05);
--shadow-md: 0 4px 6px rgba(0,0,0,0.1);
--shadow-lg: 0 10px 15px rgba(0,0,0,0.1);
```

---

## Border Radius

### Radius Scale

| Name | Value | Tailwind | CSS Variable | Usage |
|------|-------|----------|--------------|-------|
| none | 0 | `rounded-none` | - | Sharp corners |
| sm | 0.125rem (2px) | `rounded-sm` | `--radius-sm` | Subtle rounding |
| default | 0.25rem (4px) | `rounded` | - | Inputs, small elements |
| md | 0.375rem (6px) | `rounded-md` | - | Buttons, badges |
| lg | 0.5rem (8px) | `rounded-lg` | `--radius` | Cards, containers |
| xl | 0.75rem (12px) | `rounded-xl` | `--radius-lg` | Large cards, modals |
| 2xl | 1rem (16px) | `rounded-2xl` | - | Feature cards |
| full | 9999px | `rounded-full` | - | Avatars, pills |

### CSS Variables (shadcn/ui)

```css
--radius: 0.5rem;
--radius-sm: 0.25rem;
--radius-lg: 0.75rem;
```

### Usage Examples

```tsx
// Buttons
<Button className="rounded-md" />

// Cards
<Card className="rounded-lg" />

// Avatars
<Avatar className="rounded-full" />

// Input fields
<Input className="rounded-md" />
```

---

## Z-Index Scale

### Z-Index Layers

| Name | Value | Tailwind | Usage |
|------|-------|----------|-------|
| auto | auto | `z-auto` | Default stacking |
| 0 | 0 | `z-0` | Base layer |
| 10 | 10 | `z-10` | Elevated content |
| 20 | 20 | `z-20` | Dropdowns |
| 30 | 30 | `z-30` | Fixed headers |
| 40 | 40 | `z-40` | Overlays |
| 50 | 50 | `z-50` | Modals, dialogs |

### Stacking Context Guidelines

| Layer | Z-Index Range | Components |
|-------|---------------|------------|
| Base | 0 | Page content, cards |
| Sticky | 10-20 | Sticky headers, floating buttons |
| Dropdown | 20-30 | Menus, popovers, tooltips |
| Fixed | 30-40 | Fixed navigation, sidebars |
| Overlay | 40-50 | Backdrop, dimmed backgrounds |
| Modal | 50+ | Dialogs, sheets, alerts |

### Usage Examples

```tsx
// Sticky header
<header className="sticky top-0 z-30 bg-background">

// Dropdown menu
<DropdownMenuContent className="z-20">

// Modal dialog
<DialogContent className="z-50">

// Toast notifications
<Toaster className="z-50">
```

---

## Complete CSS Variables Reference

Copy this to your `globals.css` file:

```css
@layer base {
  :root {
    /* Colors */
    --background: 0 0% 100%;
    --foreground: 222.2 84% 4.9%;
    --card: 0 0% 100%;
    --card-foreground: 222.2 84% 4.9%;
    --popover: 0 0% 100%;
    --popover-foreground: 222.2 84% 4.9%;
    --primary: 222.2 47.4% 11.2%;
    --primary-foreground: 210 40% 98%;
    --secondary: 210 40% 96.1%;
    --secondary-foreground: 222.2 47.4% 11.2%;
    --muted: 210 40% 96.1%;
    --muted-foreground: 215.4 16.3% 46.9%;
    --accent: 210 40% 96.1%;
    --accent-foreground: 222.2 47.4% 11.2%;
    --destructive: 0 84.2% 60.2%;
    --destructive-foreground: 210 40% 98%;
    --border: 214.3 31.8% 91.4%;
    --input: 214.3 31.8% 91.4%;
    --ring: 222.2 84% 4.9%;

    /* Extended semantic colors */
    --success: 142 76% 36%;
    --success-foreground: 210 40% 98%;
    --warning: 38 92% 50%;
    --warning-foreground: 222.2 84% 4.9%;
    --info: 199 89% 48%;
    --info-foreground: 210 40% 98%;

    /* Border radius */
    --radius: 0.5rem;
    --radius-sm: 0.25rem;
    --radius-lg: 0.75rem;
  }
}
```
