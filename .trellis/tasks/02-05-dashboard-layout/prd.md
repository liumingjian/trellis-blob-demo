# Admin Dashboard Layout and Navigation

## Phase
Phase 1 - MVP (Dashboard)

## Goal
Create the admin dashboard layout with navigation sidebar and header.

## Requirements
- Protected layout (auth required)
- Sidebar navigation
- User info in header
- Responsive design

## Acceptance Criteria
- [ ] Dashboard layout at `/dashboard`
- [ ] Sidebar with navigation links
- [ ] Header with user name and logout
- [ ] Active link highlighting
- [ ] Collapsible sidebar on mobile
- [ ] Redirect to login if not authenticated
- [ ] Welcome message on dashboard home

## Technical Notes
- Use Next.js layout for shared UI
- Check session in layout component
- Use shadcn/ui Sheet for mobile sidebar

## Dependencies
- setup-nextauth

## Files to Create
- `src/app/dashboard/layout.tsx`
- `src/app/dashboard/page.tsx`
- `src/components/dashboard/sidebar.tsx`
- `src/components/dashboard/header.tsx`
