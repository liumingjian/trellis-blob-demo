# Accessibility Guidelines

> WCAG 2.1 AA compliance requirements and best practices for the Blog Application.

---

## WCAG 2.1 AA Compliance

### Overview

The Blog Application targets WCAG 2.1 Level AA compliance as a baseline. This ensures the application is accessible to users with visual, auditory, motor, and cognitive disabilities.

### Four Principles (POUR)

| Principle | Description | Key Requirements |
|-----------|-------------|------------------|
| **Perceivable** | Information must be presentable to users | Text alternatives, captions, color contrast |
| **Operable** | UI must be operable by all users | Keyboard accessible, sufficient time, no seizures |
| **Understandable** | Information and UI must be understandable | Readable, predictable, input assistance |
| **Robust** | Content must work with assistive technologies | Valid HTML, ARIA support |

### Compliance Checklist

#### Perceivable

- [ ] All images have meaningful `alt` text (or `alt=""` for decorative)
- [ ] Color is not the only means of conveying information
- [ ] Text has minimum 4.5:1 contrast ratio (3:1 for large text)
- [ ] Content can be resized to 200% without loss of functionality
- [ ] No content flashes more than 3 times per second

#### Operable

- [ ] All functionality available via keyboard
- [ ] No keyboard traps exist
- [ ] Skip links provided for navigation
- [ ] Focus order is logical and intuitive
- [ ] Focus indicators are visible
- [ ] Page titles are descriptive and unique

#### Understandable

- [ ] Language is declared on the page (`lang` attribute)
- [ ] Form labels are associated with inputs
- [ ] Error messages are clear and helpful
- [ ] Navigation is consistent across pages
- [ ] Instructions don't rely solely on sensory characteristics

#### Robust

- [ ] HTML is valid and well-formed
- [ ] ARIA attributes are used correctly
- [ ] Custom components have appropriate roles
- [ ] Content works with screen readers

---

## Color Contrast

### Minimum Contrast Ratios

| Element Type | Minimum Ratio | WCAG Level |
|--------------|---------------|------------|
| Normal text (< 18px) | 4.5:1 | AA |
| Large text (>= 18px bold or >= 24px) | 3:1 | AA |
| UI components and graphics | 3:1 | AA |
| Enhanced (normal text) | 7:1 | AAA |

### Design System Contrast Verification

Our color tokens are designed to meet WCAG AA requirements:

| Combination | Contrast Ratio | Status |
|-------------|----------------|--------|
| `foreground` on `background` | ~16:1 | Pass |
| `primary-foreground` on `primary` | ~12:1 | Pass |
| `muted-foreground` on `background` | ~4.6:1 | Pass |
| `destructive-foreground` on `destructive` | ~4.5:1 | Pass |

### Testing Tools

| Tool | Usage | Link |
|------|-------|------|
| WebAIM Contrast Checker | Manual color testing | webaim.org/resources/contrastchecker |
| axe DevTools | Automated testing | Browser extension |
| Lighthouse | Audit reports | Chrome DevTools |
| Stark | Design tool plugin | Figma/Sketch plugin |

### Common Contrast Issues

```tsx
// BAD: Insufficient contrast
<p className="text-muted-foreground bg-muted">
  This may fail contrast requirements
</p>

// GOOD: Ensure sufficient contrast
<p className="text-foreground bg-muted">
  This has adequate contrast
</p>

// BAD: Placeholder text too light
<Input placeholder="Enter title" className="placeholder:text-gray-300" />

// GOOD: Accessible placeholder
<Input placeholder="Enter title" className="placeholder:text-muted-foreground" />
```

### Dark Mode Considerations

Always verify contrast in both light and dark modes:

```tsx
// Use semantic tokens that adapt to theme
<p className="text-foreground">Always readable</p>

// Avoid hardcoded colors that may fail in one mode
<p className="text-gray-700">May fail in dark mode</p>
```

---

## Keyboard Navigation

### Focus Management

All interactive elements must be keyboard accessible and have visible focus states.

#### Default Focus Ring (shadcn/ui)

```tsx
// shadcn/ui components include focus styles by default
<Button>
  {/* Includes: focus-visible:outline-none focus-visible:ring-2
      focus-visible:ring-ring focus-visible:ring-offset-2 */}
  Click Me
</Button>

// Custom focus ring for non-shadcn elements
<div
  tabIndex={0}
  className="focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 rounded-md"
>
  Focusable content
</div>
```

### Tab Order

Ensure logical tab order that follows visual layout:

```tsx
// GOOD: Natural DOM order matches visual order
<nav>
  <Link href="/">Home</Link>
  <Link href="/posts">Posts</Link>
  <Link href="/about">About</Link>
</nav>

// BAD: Using tabIndex to force order
<nav>
  <Link href="/" tabIndex={3}>Home</Link>
  <Link href="/posts" tabIndex={1}>Posts</Link>
  <Link href="/about" tabIndex={2}>About</Link>
</nav>
```

#### Tab Index Values

| Value | Behavior | Usage |
|-------|----------|-------|
| `tabIndex={0}` | Focusable in natural order | Custom interactive elements |
| `tabIndex={-1}` | Programmatically focusable only | Focus management targets |
| `tabIndex={1+}` | Avoid | Creates confusing tab order |

### Keyboard Shortcuts

Provide keyboard shortcuts for common actions, but ensure they don't conflict with assistive technology shortcuts.

```tsx
// Example: Keyboard shortcut hook
function useKeyboardShortcut(
  key: string,
  callback: () => void,
  modifier?: 'ctrl' | 'meta'
) {
  useEffect(() => {
    const handler = (e: KeyboardEvent) => {
      const modifierPressed = modifier
        ? (modifier === 'ctrl' ? e.ctrlKey : e.metaKey)
        : true

      if (e.key === key && modifierPressed) {
        e.preventDefault()
        callback()
      }
    }

    window.addEventListener('keydown', handler)
    return () => window.removeEventListener('keydown', handler)
  }, [key, callback, modifier])
}

// Usage: Cmd/Ctrl + S to save
useKeyboardShortcut('s', handleSave, 'meta')
```

#### Common Blog Shortcuts

| Action | Shortcut | Implementation |
|--------|----------|----------------|
| Save draft | Cmd/Ctrl + S | Prevent default, trigger save |
| Search | Cmd/Ctrl + K | Open search dialog |
| New post | Cmd/Ctrl + N | Navigate to new post |
| Bold text | Cmd/Ctrl + B | In editor only |

### Interactive Element Requirements

```tsx
// Buttons - use native button element
<button onClick={handleClick}>Click me</button>

// Links - use for navigation
<Link href="/posts">View posts</Link>

// Custom interactive elements - add keyboard support
<div
  role="button"
  tabIndex={0}
  onClick={handleClick}
  onKeyDown={(e) => {
    if (e.key === 'Enter' || e.key === ' ') {
      e.preventDefault()
      handleClick()
    }
  }}
>
  Custom button
</div>
```

---

## Screen Reader Support

### Semantic HTML

Use semantic HTML elements to provide structure and meaning:

```tsx
// GOOD: Semantic structure
<article>
  <header>
    <h1>Post Title</h1>
    <p>Published on <time dateTime="2024-01-15">January 15, 2024</time></p>
  </header>
  <main>
    <p>Post content...</p>
  </main>
  <footer>
    <p>Written by Author Name</p>
  </footer>
</article>

// BAD: Div soup
<div className="post">
  <div className="header">
    <div className="title">Post Title</div>
    <div className="date">January 15, 2024</div>
  </div>
  <div className="content">
    <div>Post content...</div>
  </div>
</div>
```

### Landmark Regions

```tsx
// Page structure with landmarks
<body>
  <header role="banner">
    <nav aria-label="Main navigation">
      {/* Primary navigation */}
    </nav>
  </header>

  <main role="main">
    {/* Page content */}
  </main>

  <aside role="complementary" aria-label="Related posts">
    {/* Sidebar content */}
  </aside>

  <footer role="contentinfo">
    {/* Footer content */}
  </footer>
</body>
```

### ARIA Labels

Provide accessible names for elements that need context:

```tsx
// Icon-only buttons
<Button variant="ghost" size="icon" aria-label="Open settings">
  <Settings className="h-4 w-4" />
</Button>

// Search input
<div className="relative">
  <Search className="absolute left-3 top-1/2 -translate-y-1/2 h-4 w-4 text-muted-foreground" />
  <Input
    type="search"
    placeholder="Search posts..."
    aria-label="Search posts"
    className="pl-10"
  />
</div>

// Navigation with multiple nav elements
<nav aria-label="Main navigation">
  {/* Header nav */}
</nav>
<nav aria-label="Breadcrumb">
  {/* Breadcrumb nav */}
</nav>
<nav aria-label="Pagination">
  {/* Pagination nav */}
</nav>
```

### Live Regions

Announce dynamic content changes to screen readers:

```tsx
// Status messages
<div role="status" aria-live="polite" className="sr-only">
  {statusMessage}
</div>

// Error announcements
<div role="alert" aria-live="assertive">
  {errorMessage && (
    <p className="text-destructive">{errorMessage}</p>
  )}
</div>

// Loading state
<div aria-live="polite" aria-busy={isLoading}>
  {isLoading ? (
    <p className="sr-only">Loading posts...</p>
  ) : (
    <PostList posts={posts} />
  )}
</div>
```

#### Live Region Politeness

| Value | Usage | Example |
|-------|-------|---------|
| `polite` | Non-urgent updates | "Post saved", "3 results found" |
| `assertive` | Urgent/error messages | "Error: Title required" |
| `off` | Disable announcements | Frequently updating content |

### Screen Reader Only Content

Use `.sr-only` for content that should only be read by screen readers:

```tsx
// Skip link (visible on focus)
<a
  href="#main-content"
  className="sr-only focus:not-sr-only focus:absolute focus:top-4 focus:left-4 focus:z-50 focus:px-4 focus:py-2 focus:bg-background focus:border focus:rounded-md"
>
  Skip to main content
</a>

// Additional context for screen readers
<Button>
  Delete
  <span className="sr-only">post titled "{postTitle}"</span>
</Button>

// Icon with hidden decorative element
<div className="flex items-center gap-2">
  <CheckCircle className="h-4 w-4 text-green-500" aria-hidden="true" />
  <span>Published</span>
</div>
```

---

## Focus Management

### Focus Indicators

All interactive elements must have visible focus indicators:

```tsx
// Default shadcn/ui focus ring
<Button className="focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2">
  Submit
</Button>

// Custom focus indicator for cards
<Card
  tabIndex={0}
  className="cursor-pointer focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2"
>
  <CardContent>Clickable card</CardContent>
</Card>

// High contrast focus for better visibility
<Input className="focus-visible:ring-2 focus-visible:ring-primary focus-visible:ring-offset-2" />
```

### Focus Trapping (Modals)

Trap focus within modal dialogs to prevent users from tabbing to background content:

```tsx
// shadcn/ui Dialog handles focus trapping automatically
import {
  Dialog,
  DialogContent,
  DialogHeader,
  DialogTitle,
} from "@/components/ui/dialog"

<Dialog open={isOpen} onOpenChange={setIsOpen}>
  <DialogContent>
    {/* Focus is automatically trapped here */}
    <DialogHeader>
      <DialogTitle>Edit Post</DialogTitle>
    </DialogHeader>
    <form>
      <Input autoFocus /> {/* First focusable element */}
      <Button type="submit">Save</Button>
    </form>
  </DialogContent>
</Dialog>
```

#### Focus Trap Requirements

1. Focus moves to first focusable element when modal opens
2. Tab cycles through modal content only
3. Escape key closes the modal
4. Focus returns to trigger element when modal closes

### Skip Links

Provide skip links to bypass repetitive navigation:

```tsx
// Skip link component
function SkipLink() {
  return (
    <a
      href="#main-content"
      className="
        sr-only focus:not-sr-only
        focus:absolute focus:top-4 focus:left-4 focus:z-50
        focus:px-4 focus:py-2
        focus:bg-background focus:text-foreground
        focus:border focus:rounded-md
        focus:outline-none focus:ring-2 focus:ring-ring
      "
    >
      Skip to main content
    </a>
  )
}

// Usage in layout
export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en">
      <body>
        <SkipLink />
        <Header />
        <main id="main-content" tabIndex={-1}>
          {children}
        </main>
        <Footer />
      </body>
    </html>
  )
}
```

### Focus Restoration

Return focus to the appropriate element after actions:

```tsx
// Focus restoration after delete
function PostList() {
  const deleteButtonRef = useRef<HTMLButtonElement>(null)

  const handleDelete = async (postId: string) => {
    await deletePost(postId)
    // Return focus to a logical element
    deleteButtonRef.current?.focus()
  }

  return (
    <ul>
      {posts.map((post, index) => (
        <li key={post.id}>
          <span>{post.title}</span>
          <Button
            ref={index === 0 ? deleteButtonRef : undefined}
            variant="ghost"
            onClick={() => handleDelete(post.id)}
          >
            Delete
          </Button>
        </li>
      ))}
    </ul>
  )
}
```

---

## ARIA Patterns

### Common ARIA Roles

| Role | Usage | Example |
|------|-------|---------|
| `button` | Clickable elements that aren't `<button>` | Custom button components |
| `link` | Navigational elements that aren't `<a>` | Custom link components |
| `navigation` | Navigation landmarks | Nav containers |
| `main` | Main content area | Primary content |
| `complementary` | Supporting content | Sidebars |
| `alert` | Important messages | Error notifications |
| `status` | Status updates | Success messages |
| `dialog` | Modal dialogs | Popups, modals |
| `tablist`, `tab`, `tabpanel` | Tab interfaces | Tabbed content |

### ARIA States

```tsx
// Expanded/collapsed state
<Button
  aria-expanded={isOpen}
  aria-controls="menu-content"
  onClick={() => setIsOpen(!isOpen)}
>
  Menu
</Button>
<div id="menu-content" hidden={!isOpen}>
  {/* Menu items */}
</div>

// Selected state
<div role="tablist">
  <button
    role="tab"
    aria-selected={activeTab === 'posts'}
    aria-controls="posts-panel"
    onClick={() => setActiveTab('posts')}
  >
    Posts
  </button>
</div>

// Disabled state
<Button disabled aria-disabled="true">
  Submit
</Button>

// Loading state
<Button aria-busy={isLoading} disabled={isLoading}>
  {isLoading ? 'Saving...' : 'Save'}
</Button>

// Invalid state (forms)
<Input
  aria-invalid={!!error}
  aria-describedby={error ? 'email-error' : undefined}
/>
{error && <p id="email-error" className="text-destructive">{error}</p>}
```

### ARIA Best Practices

#### Do's

```tsx
// DO: Use native HTML elements when possible
<button onClick={handleClick}>Submit</button>

// DO: Provide accessible names
<Button aria-label="Close dialog">
  <X className="h-4 w-4" />
</Button>

// DO: Associate labels with inputs
<Label htmlFor="email">Email</Label>
<Input id="email" type="email" />

// DO: Use aria-describedby for additional context
<Input
  id="password"
  type="password"
  aria-describedby="password-requirements"
/>
<p id="password-requirements" className="text-sm text-muted-foreground">
  Must be at least 8 characters
</p>
```

#### Don'ts

```tsx
// DON'T: Use ARIA when native HTML works
<div role="button" tabIndex={0}>Submit</div> // Use <button> instead

// DON'T: Override native semantics incorrectly
<button role="link">Click here</button> // Use <a> for links

// DON'T: Use aria-label on elements with visible text
<Button aria-label="Submit form">Submit</Button> // Redundant

// DON'T: Hide content from screen readers unnecessarily
<p aria-hidden="true">Important information</p> // Users miss this
```

### Form Accessibility Pattern

```tsx
// Complete accessible form example
<form onSubmit={handleSubmit} aria-label="Create new post">
  <div className="space-y-4">
    {/* Text input with label and error */}
    <div className="space-y-2">
      <Label htmlFor="title">
        Title <span aria-hidden="true" className="text-destructive">*</span>
        <span className="sr-only">(required)</span>
      </Label>
      <Input
        id="title"
        required
        aria-required="true"
        aria-invalid={!!errors.title}
        aria-describedby={errors.title ? 'title-error' : 'title-hint'}
      />
      <p id="title-hint" className="text-sm text-muted-foreground">
        Enter a descriptive title for your post
      </p>
      {errors.title && (
        <p id="title-error" role="alert" className="text-sm text-destructive">
          {errors.title}
        </p>
      )}
    </div>

    {/* Select with label */}
    <div className="space-y-2">
      <Label htmlFor="category">Category</Label>
      <Select>
        <SelectTrigger id="category" aria-label="Select a category">
          <SelectValue placeholder="Select a category" />
        </SelectTrigger>
        <SelectContent>
          <SelectItem value="tech">Technology</SelectItem>
          <SelectItem value="design">Design</SelectItem>
        </SelectContent>
      </Select>
    </div>

    {/* Submit button with loading state */}
    <Button type="submit" disabled={isSubmitting} aria-busy={isSubmitting}>
      {isSubmitting ? (
        <>
          <Loader2 className="mr-2 h-4 w-4 animate-spin" aria-hidden="true" />
          <span>Publishing...</span>
        </>
      ) : (
        'Publish Post'
      )}
    </Button>
  </div>

  {/* Form-level error announcement */}
  <div role="alert" aria-live="assertive" className="sr-only">
    {formError}
  </div>
</form>
```

---

## Testing Recommendations

### Manual Testing Checklist

| Test | Method | Pass Criteria |
|------|--------|---------------|
| Keyboard navigation | Tab through page | All interactive elements reachable |
| Focus visibility | Tab through page | Focus indicator always visible |
| Screen reader | Use NVDA/VoiceOver | Content announced correctly |
| Zoom | Browser zoom to 200% | No content loss or overlap |
| Color contrast | Use contrast checker | Meets 4.5:1 / 3:1 ratios |
| Reduced motion | Enable OS setting | Animations respect preference |

### Automated Testing Tools

```bash
# Install axe-core for automated testing
npm install -D @axe-core/react

# Install jest-axe for unit tests
npm install -D jest-axe
```

```tsx
// Component test with jest-axe
import { render } from '@testing-library/react'
import { axe, toHaveNoViolations } from 'jest-axe'

expect.extend(toHaveNoViolations)

test('PostCard has no accessibility violations', async () => {
  const { container } = render(<PostCard post={mockPost} />)
  const results = await axe(container)
  expect(results).toHaveNoViolations()
})
```

### Browser DevTools

| Tool | Browser | Usage |
|------|---------|-------|
| Lighthouse | Chrome | Accessibility audit |
| Accessibility Inspector | Firefox | Element inspection |
| axe DevTools | Chrome/Firefox | Detailed violations |
| WAVE | Chrome/Firefox | Visual feedback |

### Screen Reader Testing

| Screen Reader | Platform | Testing Focus |
|---------------|----------|---------------|
| VoiceOver | macOS/iOS | Safari compatibility |
| NVDA | Windows | Chrome/Firefox compatibility |
| JAWS | Windows | Enterprise compatibility |
| TalkBack | Android | Mobile compatibility |

---

## Quick Reference

### Essential Classes

| Purpose | Tailwind Classes |
|---------|------------------|
| Focus ring | `focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2` |
| Screen reader only | `sr-only` |
| Skip link visible on focus | `sr-only focus:not-sr-only focus:absolute focus:z-50` |
| Reduced motion | `motion-reduce:transition-none motion-reduce:animate-none` |

### Essential ARIA Attributes

| Attribute | Usage |
|-----------|-------|
| `aria-label` | Accessible name for elements without visible text |
| `aria-labelledby` | Reference to element containing accessible name |
| `aria-describedby` | Reference to element with additional description |
| `aria-expanded` | Expandable element state |
| `aria-hidden` | Hide decorative elements from screen readers |
| `aria-live` | Announce dynamic content changes |
| `aria-invalid` | Form validation state |
| `aria-required` | Required form field |

### Contrast Quick Check

| Text Type | Minimum Ratio | Check Against |
|-----------|---------------|---------------|
| Body text | 4.5:1 | Background color |
| Large text (18px+ bold) | 3:1 | Background color |
| UI components | 3:1 | Adjacent colors |
| Placeholder text | 4.5:1 | Input background |
