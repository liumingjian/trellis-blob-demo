# Configure Prisma ORM and PostgreSQL Database

## Phase
Phase 1 - MVP (Infrastructure)

## Goal
Set up Prisma ORM with PostgreSQL database, including User and Article models as defined in the PRD schema.

## Requirements
- Prisma ORM configured with PostgreSQL
- Database schema matching PRD specification
- Type-safe database client generation
- Migration workflow established

## Acceptance Criteria
- [ ] Prisma installed and initialized
- [ ] `prisma/schema.prisma` with User and Article models
- [ ] Status enum (DRAFT, PUBLISHED) defined
- [ ] Proper indexes on frequently queried fields
- [ ] `src/lib/prisma.ts` singleton client instance
- [ ] Initial migration created and applied
- [ ] `npx prisma generate` produces types
- [ ] `npx prisma studio` opens database GUI
- [ ] Seed script for development data (optional)

## Database Schema
```prisma
model User {
  id            String    @id @default(cuid())
  email         String    @unique
  passwordHash  String
  name          String?
  createdAt     DateTime  @default(now())
  updatedAt     DateTime  @updatedAt
  articles      Article[]
}

model Article {
  id          String    @id @default(cuid())
  title       String
  slug        String    @unique
  content     String    @db.Text
  excerpt     String?
  featuredImg String?
  status      Status    @default(DRAFT)
  authorId    String
  author      User      @relation(fields: [authorId], references: [id])
  createdAt   DateTime  @default(now())
  updatedAt   DateTime  @updatedAt
  publishedAt DateTime?
}

enum Status {
  DRAFT
  PUBLISHED
}
```

## Technical Notes
- Use connection pooling for production
- Add `@@index` on authorId for Article queries
- Configure Prisma logging for development

## Dependencies
- setup-nextjs-project

## Files to Create/Modify
- `prisma/schema.prisma`
- `src/lib/prisma.ts`
- `prisma/seed.ts` (optional)
- `.env` - DATABASE_URL
