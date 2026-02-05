# E2E Testing Guidelines

> End-to-end testing with agent-browser for the Blog Application.

---

## Overview

Use `agent-browser` CLI for E2E testing:
- Browser automation without Playwright boilerplate
- Snapshot-based element selection
- State persistence for auth flows

---

## Core Workflow

```bash
# 1. Navigate
agent-browser open http://localhost:3000

# 2. Snapshot (get element refs)
agent-browser snapshot -i

# 3. Interact using refs
agent-browser fill @e1 "test@example.com"
agent-browser click @e2

# 4. Re-snapshot after navigation
agent-browser snapshot -i
```

---

## Test Scenarios

### Authentication Flow

```bash
# Register
agent-browser open http://localhost:3000/register
agent-browser snapshot -i
agent-browser fill @e1 "test@example.com"
agent-browser fill @e2 "password123"
agent-browser fill @e3 "password123"
agent-browser click @e4
agent-browser wait --url "**/dashboard"

# Save auth state
agent-browser state save auth.json
```

### Login Flow

```bash
agent-browser open http://localhost:3000/login
agent-browser snapshot -i
agent-browser fill @e1 "test@example.com"
agent-browser fill @e2 "password123"
agent-browser click @e3
agent-browser wait --url "**/dashboard"
```

### Article CRUD

```bash
# Load auth state
agent-browser state load auth.json

# Create article
agent-browser open http://localhost:3000/dashboard/articles/new
agent-browser snapshot -i
agent-browser fill @e1 "Test Article Title"
agent-browser fill @e2 "Article content here..."
agent-browser click @e3  # Save button
agent-browser wait --load networkidle

# Verify created
agent-browser snapshot -i
agent-browser get text body
```

---

## Best Practices

| Practice | Reason |
|----------|--------|
| Re-snapshot after navigation | Refs invalidate on DOM change |
| Use `wait --load networkidle` | Ensure page fully loaded |
| Save auth state | Reuse across tests |
| Use semantic locators as fallback | When refs unreliable |

---

## Forbidden Patterns

| Pattern | Reason | Alternative |
|---------|--------|-------------|
| Hardcoded waits | Flaky tests | `wait --load` |
| Stale refs | Element not found | Re-snapshot |
| No error handling | Silent failures | Check results |
