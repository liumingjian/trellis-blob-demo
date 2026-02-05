# NextAuth.js Setup with Credentials Provider

## Phase
Phase 1 - MVP (Authentication)

## Goal
Configure NextAuth.js with Credentials provider for email/password authentication, including session management and protected route middleware.

## Requirements
- NextAuth.js v5 (Auth.js) configured
- Credentials provider for email/password login
- JWT session strategy with HTTP-only cookies
- Auth middleware for protected routes

## Acceptance Criteria
- [ ] NextAuth.js installed and configured
- [ ] `src/lib/auth.ts` with auth configuration
- [ ] Credentials provider with email/password validation
- [ ] JWT session with secure cookie settings
- [ ] `src/middleware.ts` protecting `/dashboard/*` routes
- [ ] `src/lib/auth-utils.ts` with helper functions
- [ ] Session includes user id, email, name
- [ ] CSRF protection enabled
- [ ] Auth API routes working (`/api/auth/*`)

## Technical Notes
- Use bcrypt for password comparison
- Session expires after 30 days
- Secure cookies in production (HTTPS only)
- Rate limiting on auth endpoints (future)

## Dependencies
- setup-prisma-database

## Files to Create/Modify
- `src/lib/auth.ts` - Auth configuration
- `src/lib/auth-utils.ts` - Helper functions
- `src/middleware.ts` - Route protection
- `src/app/api/auth/[...nextauth]/route.ts`
- `.env` - NEXTAUTH_SECRET, NEXTAUTH_URL
