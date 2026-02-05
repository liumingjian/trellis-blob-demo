# Comments System with Moderation

## Phase
Phase 3 - Future

## Goal
Implement a comments system for reader engagement with moderation capabilities.

## Requirements
- Comment submission on articles
- Nested replies support
- Admin moderation tools
- Spam prevention

## Acceptance Criteria
- [ ] Comment form on article pages
- [ ] Guest comments with name/email
- [ ] Nested replies (1 level)
- [ ] Admin approval workflow
- [ ] Delete/hide comments
- [ ] Basic spam filtering

## Database Schema
```prisma
model Comment {
  id        String    @id @default(cuid())
  content   String
  authorName String
  authorEmail String
  articleId String
  article   Article   @relation(fields: [articleId], references: [id])
  parentId  String?
  parent    Comment?  @relation("Replies", fields: [parentId], references: [id])
  replies   Comment[] @relation("Replies")
  approved  Boolean   @default(false)
  createdAt DateTime  @default(now())
}
```

## Dependencies
- Phase 1 complete
