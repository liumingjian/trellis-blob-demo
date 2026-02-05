# Setup Next.js Project with TypeScript and shadcn/ui

## Phase
Phase 1 - MVP (Infrastructure)

## Goal
Initialize a Next.js 14+ project with App Router, TypeScript strict mode, Tailwind CSS, and shadcn/ui component library as the foundation for the blog application.

## Requirements
- Next.js 14+ with App Router
- TypeScript in strict mode
- Tailwind CSS configured
- shadcn/ui initialized with default components
- ESLint and Prettier configured
- Environment variables setup with Zod validation

## Acceptance Criteria
- [ ] `npx create-next-app` with TypeScript and App Router
- [ ] Tailwind CSS working with custom theme colors
- [ ] shadcn/ui initialized (`npx shadcn-ui@latest init`)
- [ ] Basic components installed: Button, Input, Card, Form
- [ ] ESLint config with Next.js recommended rules
- [ ] Prettier config for consistent formatting
- [ ] `.env.example` file with required variables documented
- [ ] `src/lib/env.ts` with Zod schema for env validation
- [ ] Project runs without errors (`npm run dev`)
- [ ] TypeScript compiles without errors (`npm run build`)

## Technical Notes
- Use `src/` directory structure
- Configure path aliases (`@/` for `src/`)
- Set up CSS variables for theming in `globals.css`
- Use Inter font as default

## Dependencies
- None (first task)

## Files to Create/Modify
- `package.json` - dependencies
- `tsconfig.json` - TypeScript config
- `tailwind.config.ts` - Tailwind config
- `src/app/layout.tsx` - Root layout
- `src/app/page.tsx` - Home page placeholder
- `src/lib/env.ts` - Environment validation
- `components.json` - shadcn/ui config
