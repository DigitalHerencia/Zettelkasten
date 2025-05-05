---
id: ygc563dklz9cvg9q27gpeaj
title: Rules
desc: ''
updated: 1744608886056
created: 1744608886056
---
# LLM AI Coding Partner: Rules for Modern Fullstack Projects (Next.js 15 Stack)

## General Principles

- Always prioritize server-first rendering.

- Use React Server Components (RSC) by default.

- Only make components 'use client' if interaction (e.g. state, event handlers) is required.

- Keep architecture feature-driven, scalable, and modular.

## Project Structure Guidelines

- app/: Routes, pages, layouts (App Router)

- components/: Dumb, reusable UI components

- features/: Smart UI tied to logic (ex: Editor, Dashboard)

- lib/: Domain logic and infrastructure (fetching, actions, utils)

- styles/: Tailwind & CSS tokens

- types/: Shared TypeScript types

- public/: Static assets

- config/: Tailwind, Next.js, PostCSS, etc.

## Data Fetching

- Use Server Components to fetch and render server-side data.

- Do not use useEffect for data unless it’s strictly client-only.

- Use lib/fetchers/*.ts for shared fetch logic.

- Keep fetch functions async and colocated with their domain (lib/posts/getPost.ts).

## Mutations & Forms

- Use React 19 Server Actions in lib/actions/*.ts:

```ts
'use server'
export async function savePost(data: FormData) { ... }
```

- Call them via <form action={actionFn}> or actionFn() in the client.

- Use useActionState() and useFormStatus() for form state and errors.

## API Routes

- Use /app/api/* routes only for:

- Auth

- Webhooks

- 3rd-party integrations

- Public APIs

- Everything else (including CRUD) should be done via Server Actions.

### Tailwind CSS 4

- Use @import "tailwindcss" in globals.css.

- Define design tokens (--color, --radius) in CSS :root.

- Avoid extending Tailwind config with theme colors — use hsl(var(--token)) utilities instead.

- Enable darkMode: 'class'.

- React 19 Usage
- Use useOptimistic() for previews and form UX.

- Use useTransition() for async state and UI transitions.

- Use <form action={fn}> with Server Actions for mutation flows.

- Prefer use() for loading data inside Server Components.

## TypeScript 5 Best Practices

- Use satisfies to validate config objects with type safety.

- Enable strict and use const type inference where applicable.

- Use @decorators (if needed) for class/utility logic.

- Use modern as const, tuple typing, and infer when building utility types.

## Testing & Maintainability

Write reusable fetchers, actions, and UI.

- Keep concerns isolated:

- UI in components/

- Logic in lib/

- Pages in app/

- Avoid over-customizing Tailwind in tailwind.config.ts — use the new CSS-first theming.