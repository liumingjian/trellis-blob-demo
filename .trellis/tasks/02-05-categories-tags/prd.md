# Categories and Tags System

## Phase
Phase 2 - Enhancements

## Goal
Implement categories and tags for article organization and filtering.

## Requirements
- Category and Tag models
- CRUD operations for categories/tags
- Article filtering by category/tag
- Public category/tag pages

## Acceptance Criteria
- [ ] Category model with name, slug, description
- [ ] Tag model with name, slug
- [ ] Many-to-many relation: Article <-> Tag
- [ ] One-to-many relation: Category -> Article
- [ ] Category management in dashboard
- [ ] Tag management in dashboard
- [ ] Category selector in article editor
- [ ] Tag input with autocomplete
- [ ] Public `/categories/[slug]` page
- [ ] Public `/tags/[slug]` page
- [ ] Category/tag display on article cards

## Database Schema
```prisma
model Category {
  id          String    @id @default(cuid())
  name        String
  slug        String    @unique
  description String?
  articles    Article[]
}

model Tag {
  id       String    @id @default(cuid())
  name     String
  slug     String    @unique
  articles Article[]
}
```

## Dependencies
- article-crud-api (Phase 1 complete)

## Files to Create
- `src/lib/actions/category.ts`
- `src/lib/actions/tag.ts`
- `src/app/categories/[slug]/page.tsx`
- `src/app/tags/[slug]/page.tsx`
- `src/components/article/category-select.tsx`
- `src/components/article/tag-input.tsx`
