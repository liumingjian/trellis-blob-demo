# Interaction Guidelines

> Hover states, animations, loading patterns, and feedback for the Blog Application.

---

## Hover States

### Button Hover Effects

Use opacity and background color shifts for hover feedback. Avoid scale transforms to prevent layout shift.

| Variant | Hover Effect | Tailwind Classes |
|---------|--------------|------------------|
| Primary | Darken background | `hover:bg-primary/90` |
| Secondary | Darken background | `hover:bg-secondary/80` |
| Outline | Fill with accent | `hover:bg-accent hover:text-accent-foreground` |
| Ghost | Subtle background | `hover:bg-accent hover:text-accent-foreground` |
| Destructive | Darken background | `hover:bg-destructive/90` |

```tsx
// Primary button with hover
<Button className="bg-primary text-primary-foreground hover:bg-primary/90 transition-colors">
  Publish Post
</Button>

// Ghost button with hover
<Button variant="ghost" className="hover:bg-accent hover:text-accent-foreground transition-colors">
  <Settings className="h-4 w-4" />
</Button>
```

### Link Hover Styles

Links should provide clear visual feedback without disrupting reading flow.

```tsx
// Navigation link
<Link
  href="/posts"
  className="text-muted-foreground hover:text-foreground transition-colors"
>
  Posts
</Link>

// Inline content link
<a
  href="/article"
  className="text-primary underline-offset-4 hover:underline transition-all"
>
  Read more
</a>

// Footer link
<Link
  href="/privacy"
  className="text-sm text-muted-foreground hover:text-foreground transition-colors"
>
  Privacy Policy
</Link>
```

### Card Hover Interactions

Cards should indicate interactivity without causing layout shift.

```tsx
// Interactive card - shadow elevation on hover
<Card className="overflow-hidden transition-shadow hover:shadow-md cursor-pointer">
  <CardContent>
    {/* Card content */}
  </CardContent>
</Card>

// Blog post card with image
<Card className="overflow-hidden group cursor-pointer">
  <div className="aspect-video relative overflow-hidden">
    <Image
      src="/post-image.jpg"
      alt="Post thumbnail"
      fill
      className="object-cover transition-transform duration-300 group-hover:scale-105"
    />
  </div>
  <CardHeader>
    <CardTitle className="group-hover:text-primary transition-colors">
      Post Title
    </CardTitle>
  </CardHeader>
</Card>
```

### Focus States

All interactive elements must have visible focus indicators for keyboard navigation.

```tsx
// Default focus ring (shadcn/ui default)
<Button className="focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2">
  Click Me
</Button>

// Input focus
<Input className="focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2" />

// Custom focus for cards
<Card
  tabIndex={0}
  className="focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2"
>
  {/* Focusable card */}
</Card>
```

---

## Animation/Transition Guidelines

### Transition Durations

Use consistent timing for predictable, polished interactions.

| Speed | Duration | CSS Variable | Usage |
|-------|----------|--------------|-------|
| Fast | 150ms | `duration-150` | Hover states, color changes |
| Normal | 200ms | `duration-200` | Most transitions |
| Slow | 300ms | `duration-300` | Complex animations, modals |
| Slower | 500ms | `duration-500` | Page transitions, large elements |

```tsx
// Fast - hover states
<Button className="transition-colors duration-150 hover:bg-primary/90">
  Submit
</Button>

// Normal - general transitions
<div className="transition-all duration-200">
  {/* Content */}
</div>

// Slow - modal/overlay animations
<DialogContent className="transition-all duration-300">
  {/* Dialog content */}
</DialogContent>
```

### Easing Functions

| Easing | Tailwind Class | Usage |
|--------|----------------|-------|
| Ease Out | `ease-out` | Elements entering (modals opening) |
| Ease In | `ease-in` | Elements exiting (modals closing) |
| Ease In Out | `ease-in-out` | Continuous animations, hover states |
| Linear | `ease-linear` | Progress bars, loading indicators |

```tsx
// Modal enter animation
<DialogContent className="transition-all duration-300 ease-out">

// Hover transition
<Card className="transition-shadow duration-200 ease-in-out hover:shadow-md">

// Progress bar
<div className="h-2 bg-primary transition-all duration-500 ease-linear" style={{ width: `${progress}%` }} />
```

### Common Animation Patterns

#### Fade In/Out

```tsx
// Using Tailwind
<div className="animate-in fade-in duration-200">
  {/* Fading content */}
</div>

// Conditional fade
<div className={cn(
  "transition-opacity duration-200",
  isVisible ? "opacity-100" : "opacity-0"
)}>
  {/* Content */}
</div>
```

#### Slide Animations

```tsx
// Slide in from bottom (for toasts, sheets)
<div className="animate-in slide-in-from-bottom-4 duration-300">
  {/* Sliding content */}
</div>

// Slide in from right (for sidebars)
<aside className="animate-in slide-in-from-right duration-300">
  {/* Sidebar content */}
</aside>
```

#### Skeleton Pulse

```tsx
// Skeleton loading animation
<div className="animate-pulse bg-muted rounded-md h-4 w-full" />
```

### Performance Considerations

1. **Use transform and opacity** - These properties are GPU-accelerated and don't trigger layout recalculation.

```tsx
// Good - GPU accelerated
<div className="transition-transform duration-200 hover:translate-y-[-2px]">

// Avoid - triggers layout
<div className="transition-all duration-200 hover:mt-[-2px]">
```

2. **Respect reduced motion preferences** - Always provide alternatives for users who prefer reduced motion.

```css
/* In globals.css */
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

3. **Limit simultaneous animations** - Avoid animating multiple properties at once when possible.

```tsx
// Good - single property
<Button className="transition-colors duration-150">

// Use sparingly - multiple properties
<Card className="transition-all duration-200">
```

---

## Loading States

### Skeleton Loaders

Use skeleton loaders for content that takes time to load. Match the skeleton shape to the expected content.

#### Basic Skeleton

```tsx
import { Skeleton } from "@/components/ui/skeleton"

// Text skeleton
<Skeleton className="h-4 w-[250px]" />

// Avatar skeleton
<Skeleton className="h-12 w-12 rounded-full" />

// Card skeleton
<Skeleton className="h-[200px] w-full rounded-lg" />
```

#### Blog Post Card Skeleton

```tsx
function PostCardSkeleton() {
  return (
    <Card className="overflow-hidden">
      <Skeleton className="aspect-video w-full" />
      <CardHeader className="space-y-2">
        <Skeleton className="h-4 w-20" />
        <Skeleton className="h-6 w-full" />
        <Skeleton className="h-6 w-3/4" />
      </CardHeader>
      <CardContent>
        <Skeleton className="h-4 w-full" />
        <Skeleton className="h-4 w-full mt-2" />
        <Skeleton className="h-4 w-2/3 mt-2" />
      </CardContent>
    </Card>
  )
}
```

#### Post List Skeleton

```tsx
function PostListSkeleton({ count = 6 }: { count?: number }) {
  return (
    <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
      {Array.from({ length: count }).map((_, i) => (
        <PostCardSkeleton key={i} />
      ))}
    </div>
  )
}
```

### Spinner Patterns

Use spinners for actions with unknown duration. Keep them subtle and appropriately sized.

```tsx
import { Loader2 } from "lucide-react"

// Button with loading spinner
<Button disabled>
  <Loader2 className="mr-2 h-4 w-4 animate-spin" />
  Publishing...
</Button>

// Inline loading
<div className="flex items-center gap-2 text-muted-foreground">
  <Loader2 className="h-4 w-4 animate-spin" />
  <span className="text-sm">Loading comments...</span>
</div>

// Full page loading
<div className="flex items-center justify-center min-h-[400px]">
  <Loader2 className="h-8 w-8 animate-spin text-muted-foreground" />
</div>
```

### Progress Indicators

Use progress bars when the completion percentage is known.

```tsx
import { Progress } from "@/components/ui/progress"

// Determinate progress
<Progress value={66} className="w-full" />

// With label
<div className="space-y-2">
  <div className="flex justify-between text-sm">
    <span>Uploading image...</span>
    <span>66%</span>
  </div>
  <Progress value={66} />
</div>
```

### Optimistic Updates

Update the UI immediately while the server request is in progress. Revert if the request fails.

```tsx
// Example: Like button with optimistic update
function LikeButton({ postId, initialLiked }: { postId: string; initialLiked: boolean }) {
  const [liked, setLiked] = useState(initialLiked)
  const [isPending, startTransition] = useTransition()

  const handleLike = () => {
    // Optimistic update
    setLiked(!liked)

    startTransition(async () => {
      try {
        await toggleLike(postId)
      } catch {
        // Revert on error
        setLiked(liked)
      }
    })
  }

  return (
    <Button
      variant="ghost"
      size="icon"
      onClick={handleLike}
      disabled={isPending}
      className={cn(liked && "text-red-500")}
    >
      <Heart className={cn("h-5 w-5", liked && "fill-current")} />
    </Button>
  )
}
```

---

## Feedback Patterns

### Success Feedback

#### Toast Notifications

Use toasts for non-blocking success messages that don't require user action.

```tsx
import { toast } from "sonner"

// Simple success toast
toast.success("Post published successfully")

// Success with description
toast.success("Post published", {
  description: "Your post is now live and visible to readers."
})

// Success with action
toast.success("Post saved as draft", {
  action: {
    label: "View drafts",
    onClick: () => router.push("/dashboard/drafts")
  }
})
```

#### Inline Success

Use inline feedback for form submissions and immediate confirmations.

```tsx
// Inline success message
<div className="flex items-center gap-2 text-sm text-green-600 dark:text-green-400">
  <CheckCircle className="h-4 w-4" />
  <span>Changes saved successfully</span>
</div>

// Success alert
<Alert className="border-green-200 bg-green-50 dark:border-green-800 dark:bg-green-950">
  <CheckCircle className="h-4 w-4 text-green-600 dark:text-green-400" />
  <AlertTitle>Success</AlertTitle>
  <AlertDescription>
    Your profile has been updated.
  </AlertDescription>
</Alert>
```

### Error Feedback

#### Toast Errors

```tsx
// Simple error toast
toast.error("Failed to publish post")

// Error with description
toast.error("Publication failed", {
  description: "Please check your connection and try again."
})

// Error with retry action
toast.error("Failed to save changes", {
  action: {
    label: "Retry",
    onClick: () => handleSave()
  }
})
```

#### Inline Errors

```tsx
// Form field error
<div className="space-y-2">
  <Label htmlFor="title" className="text-destructive">Title</Label>
  <Input
    id="title"
    className="border-destructive focus-visible:ring-destructive"
    aria-invalid="true"
    aria-describedby="title-error"
  />
  <p id="title-error" className="text-sm text-destructive">
    Title is required
  </p>
</div>

// Error alert
<Alert variant="destructive">
  <AlertCircle className="h-4 w-4" />
  <AlertTitle>Error</AlertTitle>
  <AlertDescription>
    There was a problem submitting your form. Please try again.
  </AlertDescription>
</Alert>
```

### Warning Messages

Use warnings for potentially destructive actions or important notices.

```tsx
// Warning toast
toast.warning("You have unsaved changes")

// Warning alert
<Alert className="border-yellow-200 bg-yellow-50 dark:border-yellow-800 dark:bg-yellow-900/50">
  <AlertTriangle className="h-4 w-4 text-yellow-600 dark:text-yellow-400" />
  <AlertTitle>Warning</AlertTitle>
  <AlertDescription>
    This action cannot be undone. Please proceed with caution.
  </AlertDescription>
</Alert>

// Confirmation dialog for destructive actions
<AlertDialog>
  <AlertDialogTrigger asChild>
    <Button variant="destructive">Delete Post</Button>
  </AlertDialogTrigger>
  <AlertDialogContent>
    <AlertDialogHeader>
      <AlertDialogTitle>Are you sure?</AlertDialogTitle>
      <AlertDialogDescription>
        This will permanently delete your post. This action cannot be undone.
      </AlertDialogDescription>
    </AlertDialogHeader>
    <AlertDialogFooter>
      <AlertDialogCancel>Cancel</AlertDialogCancel>
      <AlertDialogAction className="bg-destructive text-destructive-foreground hover:bg-destructive/90">
        Delete
      </AlertDialogAction>
    </AlertDialogFooter>
  </AlertDialogContent>
</AlertDialog>
```

### Info Notifications

Use info messages for helpful tips or neutral information.

```tsx
// Info toast
toast.info("Tip: You can use Markdown in your posts")

// Info alert
<Alert>
  <Info className="h-4 w-4" />
  <AlertTitle>Note</AlertTitle>
  <AlertDescription>
    Posts are automatically saved every 30 seconds.
  </AlertDescription>
</Alert>

// Inline info
<div className="flex items-start gap-2 text-sm text-muted-foreground bg-muted p-3 rounded-md">
  <Info className="h-4 w-4 mt-0.5 shrink-0" />
  <p>Your post will be reviewed before publication.</p>
</div>
```

---

## Forbidden Patterns

| Pattern | Reason |
|---------|--------|
| Scale on hover (cards) | Causes layout shift |
| Duration > 500ms | Feels slow and unresponsive |
| No feedback | Unclear state, poor UX |
| Blocking spinners | Prevents user interaction |
| Auto-playing animations | Distracting, accessibility issue |

---

## Quick Reference

### Transition Classes

| Pattern | Classes |
|---------|---------|
| Color change | `transition-colors duration-150` |
| Shadow change | `transition-shadow duration-200` |
| Transform | `transition-transform duration-200` |
| Opacity | `transition-opacity duration-200` |
| All properties | `transition-all duration-200` |

### Loading Components

| State | Component | Usage |
|-------|-----------|-------|
| Content loading | `<Skeleton />` | Page content, cards |
| Action pending | `<Loader2 className="animate-spin" />` | Buttons, inline |
| Known progress | `<Progress />` | File uploads, multi-step |

### Feedback Summary

| Type | Method | Duration |
|------|--------|----------|
| Success | Toast | Auto-dismiss (4s) |
| Error | Toast + Inline | Persist until resolved |
| Warning | Alert/Dialog | User dismisses |
| Info | Toast/Inline | Auto-dismiss (4s) |
