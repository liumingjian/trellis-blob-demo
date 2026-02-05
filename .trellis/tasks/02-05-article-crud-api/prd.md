# Article CRUD API with Server Actions

## Phase
Phase 1 - MVP (Article Management)

## Goal
Implement server actions for complete article CRUD operations with proper validation and authorization.

## Requirements
- Create, Read, Update, Delete operations
- Draft/Published status management
- Auto-generated URL slugs
- Authorization checks

## Acceptance Criteria
- [ ] `createArticle` - creates new article as draft
- [ ] `updateArticle` - updates existing article
- [ ] `deleteArticle` - soft delete (mark as deleted)
- [ ] `publishArticle` - changes status to PUBLISHED
- [ ] `unpublishArticle` - changes status to DRAFT
- [ ] `getArticle` - fetch single article by id or slug
- [ ] `getArticles` - fetch paginated list with filters
- [ ] Slug auto-generated from title
- [ ] Slug uniqueness enforced
- [ ] Only author can modify their articles
- [ ] Zod validation for all inputs

## Technical Notes
- Use slugify library for slug generation
- Handle slug conflicts with numeric suffix
- Set publishedAt when publishing
- Clear publishedAt when unpublishing

## Dependencies
- setup-prisma-database

## Files to Create/Modify
- `src/lib/actions/article.ts` - Server actions
- `src/lib/validations/article.ts` - Zod schemas
- `src/lib/utils/slug.ts` - Slug generation
