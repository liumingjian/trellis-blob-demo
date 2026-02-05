# Style Guidelines

> Visual style patterns and component styling for the Blog Application.

---

## Design Direction

**Style:** Modern Minimalist
**Tone:** Clean, professional, readable

---

## Do's

| Element | Pattern |
|---------|---------|
| Cards | Subtle shadow, rounded corners |
| Buttons | Clear hierarchy, hover feedback |
| Icons | SVG from Lucide, consistent size |
| Images | Rounded corners, aspect ratio |

---

## Don'ts

| Pattern | Reason |
|---------|--------|
| Emoji as icons | Unprofessional |
| Purple gradients | Generic AI look |
| Inter/Arial fonts | Overused |
| Scale on hover | Layout shift |

---

## Component Styling Patterns

### Button Styles

shadcn/ui provides a comprehensive button system. Use these variants consistently.

#### Primary Button

The main call-to-action button. Use sparingly for the most important actions.

```tsx
import { Button } from "@/components/ui/button"

// Primary - Main CTAs (Submit, Save, Publish)
<Button>Publish Post</Button>

// Tailwind classes applied:
// bg-primary text-primary-foreground hover:bg-primary/90
// h-10 px-4 py-2 rounded-md font-medium
```

#### Secondary Button

For secondary actions that complement primary actions.

```tsx
// Secondary - Supporting actions (Cancel, Back)
<Button variant="secondary">Save Draft</Button>

// Tailwind classes applied:
// bg-secondary text-secondary-foreground hover:bg-secondary/80
```

#### Outline Button

For tertiary actions or when you need a lighter visual weight.

```tsx
// Outline - Tertiary actions, filters
<Button variant="outline">Filter Posts</Button>

// Tailwind classes applied:
// border border-input bg-background hover:bg-accent hover:text-accent-foreground
```

#### Ghost Button

For subtle actions, often used in toolbars or navigation.

```tsx
// Ghost - Subtle actions, icon buttons
<Button variant="ghost">
  <Settings className="h-4 w-4" />
</Button>

// Tailwind classes applied:
// hover:bg-accent hover:text-accent-foreground
```

#### Destructive Button

For dangerous or irreversible actions.

```tsx
// Destructive - Delete, remove actions
<Button variant="destructive">Delete Post</Button>

// Tailwind classes applied:
// bg-destructive text-destructive-foreground hover:bg-destructive/90
```

#### Button Sizes

```tsx
<Button size="sm">Small</Button>      // h-9 px-3 text-sm
<Button size="default">Default</Button> // h-10 px-4 py-2
<Button size="lg">Large</Button>      // h-11 px-8 text-lg
<Button size="icon">              // h-10 w-10 (square)
  <Plus className="h-4 w-4" />
</Button>
```

---

### Card Patterns

Cards are the primary container for blog content.

#### Basic Card

```tsx
import { Card, CardHeader, CardTitle, CardDescription, CardContent, CardFooter } from "@/components/ui/card"

<Card className="overflow-hidden">
  <CardHeader>
    <CardTitle>Post Title</CardTitle>
    <CardDescription>Published on January 15, 2024</CardDescription>
  </CardHeader>
  <CardContent>
    <p>Post excerpt or content goes here...</p>
  </CardContent>
  <CardFooter className="flex justify-between">
    <Button variant="ghost">Read More</Button>
    <Button variant="outline" size="icon">
      <Bookmark className="h-4 w-4" />
    </Button>
  </CardFooter>
</Card>
```

#### Blog Post Card

```tsx
<Card className="overflow-hidden hover:shadow-md transition-shadow">
  <div className="aspect-video relative">
    <Image
      src="/post-image.jpg"
      alt="Post thumbnail"
      fill
      className="object-cover"
    />
  </div>
  <CardHeader className="space-y-2">
    <div className="flex items-center gap-2 text-sm text-muted-foreground">
      <span>Technology</span>
      <span>-</span>
      <time>Jan 15, 2024</time>
    </div>
    <CardTitle className="line-clamp-2">
      Building Modern Web Applications
    </CardTitle>
  </CardHeader>
  <CardContent>
    <p className="text-muted-foreground line-clamp-3">
      Post excerpt that provides a brief overview...
    </p>
  </CardContent>
</Card>
```

#### Card Variants

| Variant | Classes | Usage |
|---------|---------|-------|
| Default | `rounded-lg border bg-card` | Standard content cards |
| Elevated | `rounded-lg border bg-card shadow-md` | Featured content |
| Interactive | `rounded-lg border bg-card hover:shadow-md transition-shadow cursor-pointer` | Clickable cards |
| Muted | `rounded-lg bg-muted` | Background sections |

---

### Form Element Styling

#### Input Fields

```tsx
import { Input } from "@/components/ui/input"
import { Label } from "@/components/ui/label"

// Standard input with label
<div className="space-y-2">
  <Label htmlFor="title">Post Title</Label>
  <Input
    id="title"
    placeholder="Enter your post title"
    className="w-full"
  />
</div>

// Input with error state
<div className="space-y-2">
  <Label htmlFor="email" className="text-destructive">Email</Label>
  <Input
    id="email"
    className="border-destructive focus-visible:ring-destructive"
  />
  <p className="text-sm text-destructive">Please enter a valid email</p>
</div>
```

#### Textarea

```tsx
import { Textarea } from "@/components/ui/textarea"

<div className="space-y-2">
  <Label htmlFor="content">Content</Label>
  <Textarea
    id="content"
    placeholder="Write your post content..."
    className="min-h-[200px] resize-y"
  />
</div>
```

#### Select

```tsx
import { Select, SelectContent, SelectItem, SelectTrigger, SelectValue } from "@/components/ui/select"

<div className="space-y-2">
  <Label>Category</Label>
  <Select>
    <SelectTrigger className="w-full">
      <SelectValue placeholder="Select a category" />
    </SelectTrigger>
    <SelectContent>
      <SelectItem value="technology">Technology</SelectItem>
      <SelectItem value="design">Design</SelectItem>
      <SelectItem value="lifestyle">Lifestyle</SelectItem>
    </SelectContent>
  </Select>
</div>
```

#### Form Layout Pattern

```tsx
<form className="space-y-6">
  <div className="space-y-4">
    <div className="space-y-2">
      <Label>Title</Label>
      <Input />
    </div>
    <div className="space-y-2">
      <Label>Description</Label>
      <Textarea />
    </div>
  </div>

  <div className="flex justify-end gap-4">
    <Button variant="outline">Cancel</Button>
    <Button>Submit</Button>
  </div>
</form>
```

---

### Navigation Patterns

#### Main Navigation

```tsx
<nav className="border-b bg-background/95 backdrop-blur supports-[backdrop-filter]:bg-background/60">
  <div className="container flex h-16 items-center justify-between">
    <Link href="/" className="flex items-center gap-2 font-bold text-xl">
      <span>BlogApp</span>
    </Link>

    <div className="hidden md:flex items-center gap-6">
      <Link
        href="/posts"
        className="text-sm font-medium text-muted-foreground hover:text-foreground transition-colors"
      >
        Posts
      </Link>
      <Link
        href="/categories"
        className="text-sm font-medium text-muted-foreground hover:text-foreground transition-colors"
      >
        Categories
      </Link>
    </div>

    <div className="flex items-center gap-4">
      <Button variant="ghost" size="icon">
        <Search className="h-5 w-5" />
      </Button>
      <Button>Sign In</Button>
    </div>
  </div>
</nav>
```

#### Sidebar Navigation

```tsx
<aside className="w-64 border-r bg-muted/40 p-6">
  <nav className="space-y-2">
    <Link
      href="/dashboard"
      className="flex items-center gap-3 rounded-lg px-3 py-2 text-muted-foreground hover:bg-accent hover:text-accent-foreground transition-colors"
    >
      <Home className="h-4 w-4" />
      Dashboard
    </Link>
    <Link
      href="/dashboard/posts"
      className="flex items-center gap-3 rounded-lg bg-accent px-3 py-2 text-accent-foreground"
    >
      <FileText className="h-4 w-4" />
      Posts
    </Link>
  </nav>
</aside>
```

---

## Layout Principles

### Container Widths

| Container Type | Max Width | Usage |
|----------------|-----------|-------|
| Default | 1400px | General page layouts |
| Narrow | 768px | Blog post content, forms |
| Wide | 1600px | Dashboard, data tables |
| Full | 100% | Hero sections, full-bleed images |

```tsx
// Container usage
<div className="container">
  {/* Default container - max-w-[1400px] */}
</div>

<div className="container max-w-3xl">
  {/* Narrow container for reading - 768px */}
</div>

<article className="prose prose-lg mx-auto max-w-prose">
  {/* Optimal reading width - ~65ch */}
</article>
```

---

### Grid Systems

#### Blog Post Grid

```tsx
<div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
  {posts.map((post) => (
    <PostCard key={post.id} post={post} />
  ))}
</div>
```

#### Dashboard Layout

```tsx
<div className="grid grid-cols-1 lg:grid-cols-[280px_1fr] min-h-screen">
  <aside className="border-r bg-muted/40">
    {/* Sidebar */}
  </aside>
  <main className="p-6">
    {/* Main content */}
  </main>
</div>
```

#### Content with Sidebar

```tsx
<div className="container">
  <div className="grid grid-cols-1 lg:grid-cols-[1fr_300px] gap-8">
    <article className="prose prose-lg">
      {/* Post content */}
    </article>
    <aside className="space-y-6">
      {/* Related posts, author info */}
    </aside>
  </div>
</div>
```

---

### Responsive Breakpoints

| Breakpoint | Min Width | Tailwind Prefix | Usage |
|------------|-----------|-----------------|-------|
| Mobile | 0px | (default) | Base styles, single column |
| sm | 640px | `sm:` | Large phones |
| md | 768px | `md:` | Tablets, 2-column layouts |
| lg | 1024px | `lg:` | Laptops, sidebars appear |
| xl | 1280px | `xl:` | Desktops, full layouts |
| 2xl | 1536px | `2xl:` | Large screens |

#### Mobile-First Pattern

```tsx
<div className="
  px-4          // Mobile: 16px padding
  md:px-6       // Tablet: 24px padding
  lg:px-8       // Desktop: 32px padding
">
  <h1 className="
    text-2xl      // Mobile: smaller heading
    md:text-3xl   // Tablet: medium heading
    lg:text-4xl   // Desktop: large heading
  ">
    Page Title
  </h1>
</div>
```

---

## Visual Hierarchy

### Heading Hierarchy

| Level | Size | Weight | Margin Top | Margin Bottom |
|-------|------|--------|------------|---------------|
| h1 | text-4xl | font-bold | - | mb-8 |
| h2 | text-3xl | font-semibold | mt-12 | mb-6 |
| h3 | text-2xl | font-semibold | mt-8 | mb-4 |
| h4 | text-xl | font-semibold | mt-6 | mb-3 |
| h5 | text-lg | font-medium | mt-4 | mb-2 |
| h6 | text-base | font-medium | mt-4 | mb-2 |

```tsx
<main>
  <h1 className="text-4xl font-bold tracking-tight">
    Blog Posts
  </h1>

  <section>
    <h2 className="text-3xl font-semibold tracking-tight mt-12 mb-6">
      Featured Posts
    </h2>

    <article>
      <h3 className="text-2xl font-semibold mb-4">
        Post Title
      </h3>
    </article>
  </section>
</main>
```

---

### Content Emphasis Techniques

#### Text Emphasis

```tsx
// Primary text
<p className="text-foreground">Main content text.</p>

// Secondary text
<p className="text-muted-foreground">Metadata, timestamps.</p>

// Emphasized text
<p className="font-medium">Slightly emphasized.</p>

// Strong emphasis
<strong className="font-semibold">Important information.</strong>
```

#### Visual Emphasis

```tsx
// Highlighted content block
<div className="bg-muted rounded-lg p-4 border-l-4 border-primary">
  <p className="font-medium">Important Note</p>
  <p className="text-muted-foreground">This content needs attention.</p>
</div>

// Featured badge
<span className="inline-flex items-center rounded-full bg-primary/10 px-2.5 py-0.5 text-xs font-medium text-primary">
  Featured
</span>

// Status indicators
<span className="inline-flex items-center gap-1.5">
  <span className="h-2 w-2 rounded-full bg-green-500" />
  <span className="text-sm text-muted-foreground">Published</span>
</span>
```

---

### Whitespace Usage

| Context | Spacing | Tailwind |
|---------|---------|----------|
| Between paragraphs | 16px | `space-y-4` |
| Between sections | 48-64px | `py-12`, `py-16` |
| Card internal padding | 24px | `p-6` |
| List item spacing | 8-12px | `space-y-2`, `space-y-3` |
| Icon to text | 8px | `gap-2` |
| Button group | 12-16px | `gap-3`, `gap-4` |

---

## Dark/Light Mode

### Theme Switching Approach

Use next-themes for seamless theme switching with shadcn/ui.

#### Setup

```tsx
// app/providers.tsx
"use client"

import { ThemeProvider } from "next-themes"

export function Providers({ children }: { children: React.ReactNode }) {
  return (
    <ThemeProvider
      attribute="class"
      defaultTheme="system"
      enableSystem
      disableTransitionOnChange
    >
      {children}
    </ThemeProvider>
  )
}
```

#### Theme Toggle Component

```tsx
"use client"

import { Moon, Sun } from "lucide-react"
import { useTheme } from "next-themes"
import { Button } from "@/components/ui/button"
import {
  DropdownMenu,
  DropdownMenuContent,
  DropdownMenuItem,
  DropdownMenuTrigger,
} from "@/components/ui/dropdown-menu"

export function ThemeToggle() {
  const { setTheme } = useTheme()

  return (
    <DropdownMenu>
      <DropdownMenuTrigger asChild>
        <Button variant="ghost" size="icon">
          <Sun className="h-5 w-5 rotate-0 scale-100 transition-all dark:-rotate-90 dark:scale-0" />
          <Moon className="absolute h-5 w-5 rotate-90 scale-0 transition-all dark:rotate-0 dark:scale-100" />
          <span className="sr-only">Toggle theme</span>
        </Button>
      </DropdownMenuTrigger>
      <DropdownMenuContent align="end">
        <DropdownMenuItem onClick={() => setTheme("light")}>
          Light
        </DropdownMenuItem>
        <DropdownMenuItem onClick={() => setTheme("dark")}>
          Dark
        </DropdownMenuItem>
        <DropdownMenuItem onClick={() => setTheme("system")}>
          System
        </DropdownMenuItem>
      </DropdownMenuContent>
    </DropdownMenu>
  )
}
```

---

### Color Adjustments for Dark Mode

Define dark mode colors in `globals.css`:

```css
@layer base {
  :root {
    --background: 0 0% 100%;
    --foreground: 222.2 84% 4.9%;
    --card: 0 0% 100%;
    --card-foreground: 222.2 84% 4.9%;
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
  }

  .dark {
    --background: 222.2 84% 4.9%;
    --foreground: 210 40% 98%;
    --card: 222.2 84% 4.9%;
    --card-foreground: 210 40% 98%;
    --primary: 210 40% 98%;
    --primary-foreground: 222.2 47.4% 11.2%;
    --secondary: 217.2 32.6% 17.5%;
    --secondary-foreground: 210 40% 98%;
    --muted: 217.2 32.6% 17.5%;
    --muted-foreground: 215 20.2% 65.1%;
    --accent: 217.2 32.6% 17.5%;
    --accent-foreground: 210 40% 98%;
    --destructive: 0 62.8% 30.6%;
    --destructive-foreground: 210 40% 98%;
    --border: 217.2 32.6% 17.5%;
    --input: 217.2 32.6% 17.5%;
    --ring: 212.7 26.8% 83.9%;
  }
}
```

#### Dark Mode Considerations

| Element | Light Mode | Dark Mode | Notes |
|---------|------------|-----------|-------|
| Background | White | Near-black | Reduce eye strain |
| Text | Near-black | Off-white | Avoid pure white |
| Borders | Light gray | Dark gray | Subtle separation |
| Shadows | Visible | Reduced | Less effective in dark |
| Images | Normal | Consider dimming | Prevent glare |

#### Best Practices

```tsx
// DO: Use semantic color tokens
<div className="bg-background text-foreground">
  <p className="text-muted-foreground">Secondary text</p>
</div>

// DON'T: Use hardcoded colors
<div className="bg-white text-black">
  <p className="text-gray-500">Won't adapt to dark mode</p>
</div>

// Image brightness adjustment
<Image
  src="/hero.jpg"
  alt="Hero"
  className="dark:brightness-90"
/>
```

---

## Quick Reference

### Common Component Classes

| Component | Base Classes |
|-----------|--------------|
| Page container | `container py-12` |
| Section | `space-y-8` |
| Card | `rounded-lg border bg-card p-6` |
| Form | `space-y-6` |
| Form field | `space-y-2` |
| Button group | `flex gap-4` |
| Nav link | `text-sm font-medium text-muted-foreground hover:text-foreground transition-colors` |

### Responsive Patterns

```tsx
// Hide on mobile, show on desktop
<div className="hidden md:block">Desktop only</div>

// Show on mobile, hide on desktop
<div className="md:hidden">Mobile only</div>

// Responsive text
<h1 className="text-2xl md:text-3xl lg:text-4xl">Responsive Heading</h1>

// Responsive grid
<div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
```
