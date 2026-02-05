# Public Home Page with Article List

## Phase
Phase 1 - MVP (Public Pages)

## Goal
Create the public home page displaying a paginated list of published articles.

## Requirements
- Article list with pagination
- Only published articles visible
- Responsive grid layout
- Article card with preview info

## Acceptance Criteria
- [ ] Home page at `/`
- [ ] Displays published articles only
- [ ] 10 articles per page
- [ ] Sorted by publish date (newest first)
- [ ] Article card shows: title, excerpt, date, featured image
- [ ] Pagination controls (prev/next)
- [ ] Responsive grid (1 col mobile, 2 col tablet, 3 col desktop)
- [ ] Loading state while fetching
- [ ] Empty state when no articles

## Technical Notes
- Use Server Components for initial render
- Implement cursor-based pagination
- Optimize images with next/image

## Dependencies
- article-crud-api

## Files to Create
- `src/app/page.tsx` - Home page
- `src/components/article/article-card.tsx`
- `src/components/article/article-list.tsx`
- `src/components/ui/pagination.tsx`
