# Article Editor Page with Rich Text and Image Upload

## Phase
Phase 1 - MVP (Dashboard)

## Goal
Create the article editor page combining rich text editing and image upload for creating and editing articles.

## Requirements
- Create and edit article forms
- Rich text editor integration
- Featured image upload
- Auto-save functionality
- Draft/Publish options

## Acceptance Criteria
- [ ] New article page at `/dashboard/articles/new`
- [ ] Edit article page at `/dashboard/articles/[id]/edit`
- [ ] Title input field
- [ ] Rich text editor for content
- [ ] Featured image uploader
- [ ] Excerpt textarea (optional)
- [ ] Save as Draft button
- [ ] Publish button
- [ ] Auto-save every 30 seconds
- [ ] Unsaved changes warning on leave
- [ ] Success toast on save

## Technical Notes
- Use controlled form with react-hook-form
- Debounce auto-save to prevent excessive calls
- Use beforeunload event for unsaved warning

## Dependencies
- rich-text-editor
- image-upload
- dashboard-layout

## Files to Create
- `src/app/dashboard/articles/new/page.tsx`
- `src/app/dashboard/articles/[id]/edit/page.tsx`
- `src/components/dashboard/article-form.tsx`
