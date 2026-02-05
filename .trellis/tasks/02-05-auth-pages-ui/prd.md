# Authentication Pages UI

## Phase
Phase 1 - MVP (Public Pages)

## Goal
Create consistent, user-friendly authentication pages for login, register, and password reset flows.

## Requirements
- Consistent design across all auth pages
- Form validation feedback
- Loading states during submission
- Error message display

## Acceptance Criteria
- [ ] Login page at `/auth/login`
- [ ] Register page at `/auth/register`
- [ ] Forgot password page at `/auth/forgot-password`
- [ ] Reset password page at `/auth/reset-password`
- [ ] Consistent card-based layout
- [ ] Form validation with inline errors
- [ ] Loading spinner during submission
- [ ] Links between auth pages
- [ ] Redirect authenticated users away

## Technical Notes
- Use shadcn/ui Card, Form, Input components
- Implement useFormState for server action feedback
- Center layout with max-width container

## Dependencies
- user-login
- user-registration
- password-reset

## Files to Create
- `src/app/auth/layout.tsx` - Auth layout
- `src/app/auth/login/page.tsx`
- `src/app/auth/register/page.tsx`
- `src/app/auth/forgot-password/page.tsx`
- `src/app/auth/reset-password/page.tsx`
