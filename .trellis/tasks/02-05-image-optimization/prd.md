# Image Optimization and CDN Integration

## Phase
Phase 2 - Enhancements

## Goal
Optimize image delivery with Next.js Image component and optional CDN integration.

## Requirements
- Next.js Image optimization
- Lazy loading for images
- Responsive image sizes
- WebP format conversion

## Acceptance Criteria
- [ ] All images use next/image component
- [ ] Lazy loading enabled by default
- [ ] Responsive srcset generated
- [ ] WebP format served when supported
- [ ] Blur placeholder for images
- [ ] Image dimension validation on upload

## Dependencies
- image-upload (Phase 1)

## Files to Modify
- `src/components/article/article-card.tsx`
- `src/components/article/article-content.tsx`
- `next.config.js` - image domains
