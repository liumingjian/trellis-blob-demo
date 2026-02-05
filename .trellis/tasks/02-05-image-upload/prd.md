# Image Upload with Local Storage

## Phase
Phase 1 - MVP (Article Management)

## Goal
Implement image upload functionality for article featured images with local filesystem storage.

## Requirements
- File upload API endpoint
- Format validation (JPG, PNG, WebP, GIF)
- Size limit enforcement (5MB)
- Local filesystem storage

## Acceptance Criteria
- [ ] Upload API at `/api/upload`
- [ ] Accepts JPG, PNG, WebP, GIF formats
- [ ] Rejects files over 5MB
- [ ] Stores files in `public/uploads/`
- [ ] Returns uploaded file URL
- [ ] Unique filename generation (UUID)
- [ ] Upload progress indicator component
- [ ] Error messages for invalid files
- [ ] Image preview after upload

## Technical Notes
- Use formidable or built-in formData
- Generate UUID filenames to prevent conflicts
- Create uploads directory if not exists
- Consider image resizing (future)

## Dependencies
- setup-nextjs-project

## Files to Create
- `src/app/api/upload/route.ts`
- `src/components/upload/image-uploader.tsx`
- `src/lib/upload.ts` - Upload utilities
- `public/uploads/.gitkeep`
