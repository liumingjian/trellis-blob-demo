# Analytics Dashboard with View Counts

## Phase
Phase 3 - Future

## Goal
Implement basic analytics to track article views.

## Requirements
- View count tracking
- Analytics dashboard
- Popular articles report

## Acceptance Criteria
- [ ] Track page views per article
- [ ] Dashboard shows view counts
- [ ] Popular articles list
- [ ] Views over time chart

## Database Addition
```prisma
model PageView {
  id        String   @id @default(cuid())
  articleId String
  article   Article  @relation(fields: [articleId], references: [id])
  createdAt DateTime @default(now())
}
```

## Dependencies
- Phase 1 complete
