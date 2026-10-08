---
name: opinionated-code-structure
description: Organize functions and helper files in top-down reading order with useful one-sentence comments. Use when writing, editing, or refactoring code that defines functions.
---

# Opinionated code structure

Write code as a top-down explanation:

1. Place the main operation first.
2. Follow it with the medium-sized functions it calls.
3. Place the smallest supporting functions last.
4. Give every function a one-sentence comment stating its purpose, guarantee, or business reason.

Make each comment add information beyond the function name:

```ts
// Keeps account matching stable across casing and surrounding whitespace.
function normalizeEmail(email: string) {
  return email.trim().toLowerCase()
}
```

Apply the same order and comment rule in separate helper files.
