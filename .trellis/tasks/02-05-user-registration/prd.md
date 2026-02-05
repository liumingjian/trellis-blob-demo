# User Registration with Email and Password

## Phase
Phase 1 - MVP (Authentication)

## Goal
Implement user registration functionality allowing new users to create an account with email and password.

## Requirements
- Registration form with validation
- Password hashing before storage
- Email uniqueness check
- Success redirect to dashboard

## Acceptance Criteria
- [ ] Registration form with email, password, confirm password
- [ ] Client-side validation with Zod
- [ ] Server action for user creation
- [ ] Password hashed with bcrypt (12 rounds)
- [ ] Email uniqueness validation
- [ ] Password minimum 8 characters
- [ ] Error messages for invalid input
- [ ] Success redirects to `/dashboard`
- [ ] Auto-login after registration

## Technical Notes
- Use server actions for form submission
- Validate on both client and server
- Never log or expose password values

## Dependencies
- setup-nextauth

## Files to Create/Modify
- `src/app/auth/register/page.tsx`
- `src/components/auth/register-form.tsx`
- `src/lib/actions/auth.ts` - register action
- `src/lib/validations/auth.ts` - Zod schemas
