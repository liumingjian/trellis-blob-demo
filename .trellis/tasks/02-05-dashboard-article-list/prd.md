# Dashboard Article List with Management Actions

## Phase
Phase 1 - MVP (Dashboard)

## Goal
Create the article management list page with edit, delete, and status actions.

## Requirements
- Table view of all user's articles
- Status badges (Draft/Published)
- Edit and delete actions
- Filter by status

## Acceptance Criteria
- [ ] Article list at `/dashboard/articles`
- [ ] Table with columns: title, status, date, actions
- [ ] Status badge (Draft=yellow, Published=green)
- [ ] Edit button links to edit page
- [ ] Delete button with confirmation dialog
- [ ] Quick publish/unpublish toggle
- [ ] Filter dropdown (All, Draft, Published)
- [ ] Empty state when no articles
- [ ] "New Article" button

## Technical Notes
- Use shadcn/ui Table component
- Implement optimistic updates for status toggle
- Use AlertDialog for delete confirmation

## Dependencies
- article-crud-api
- dashboard-layout

## Files to Create
- `src/app/dashboard/articles/page.tsx`
- `src/components/dashboard/article-table.tsx`
- `src/components/dashboard/article-actions.tsx`
