# Password Reset Flow with Email

## Phase
Phase 1 - MVP (Authentication)

## Goal
Implement password reset functionality allowing users to reset their password via email link.

## Requirements
- Forgot password request form
- Reset token generation and storage
- Email sending with reset link
- Password reset form with token validation

## Acceptance Criteria
- [ ] "Forgot password" link on login page
- [ ] Email input form for reset request
- [ ] Reset token generated (secure random)
- [ ] Token stored with 1-hour expiration
- [ ] Email sent with reset link
- [ ] Reset form validates token
- [ ] New password must meet requirements
- [ ] Success redirects to login
- [ ] Expired token shows error message

## Technical Notes
- Use crypto.randomBytes for token generation
- Store hashed token in database
- Consider using Resend or Nodemailer for emails
- Rate limit reset requests per email

## Database Addition
```prisma
model PasswordResetToken {
  id        String   @id @default(cuid())
  token     String   @unique
  userId    String
  user      User     @relation(fields: [userId], references: [id])
  expiresAt DateTime
  createdAt DateTime @default(now())
}
```

## Dependencies
- user-login

## Files to Create/Modify
- `src/app/auth/forgot-password/page.tsx`
- `src/app/auth/reset-password/page.tsx`
- `src/components/auth/forgot-password-form.tsx`
- `src/components/auth/reset-password-form.tsx`
- `src/lib/actions/password-reset.ts`
- `src/lib/email.ts` - Email sending utility
- `prisma/schema.prisma` - Add PasswordResetToken
