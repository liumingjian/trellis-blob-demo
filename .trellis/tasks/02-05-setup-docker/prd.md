# Docker Configuration for Development and Production

## Phase
Phase 1 - MVP (Infrastructure)

## Goal
Create Docker configuration for both development and production environments, enabling consistent deployment across different systems.

## Requirements
- Multi-stage Dockerfile for optimized production builds
- Docker Compose for local development with PostgreSQL
- Environment variable management
- Volume mounts for development hot-reload

## Acceptance Criteria
- [ ] `Dockerfile` with multi-stage build (deps, builder, runner)
- [ ] `docker-compose.yml` for development environment
- [ ] `docker-compose.prod.yml` for production environment
- [ ] PostgreSQL service configured in compose
- [ ] Health checks for all services
- [ ] `.dockerignore` to exclude unnecessary files
- [ ] `docker compose up` starts dev environment successfully
- [ ] `docker compose -f docker-compose.prod.yml up` works
- [ ] Hot-reload works in development mode

## Technical Notes
- Use Node.js 20 Alpine as base image
- Standalone output for smaller production image
- Named volumes for PostgreSQL data persistence
- Network isolation between services

## Dependencies
- setup-nextjs-project

## Files to Create
- `Dockerfile`
- `docker-compose.yml`
- `docker-compose.prod.yml`
- `.dockerignore`
