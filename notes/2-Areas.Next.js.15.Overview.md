---
id: 56ro5o5it6dxbcbds4ehfsh
title: Overvie
desc: ''
updated: 1744608831500
created: 1744608831500
---

# 1. Project Structure: Where Should Stuff Live?

```plaintext
my-app/
├── app/                # App Router entry points
│   ├── layout.tsx      # Shared layout (headers, theme, etc.)
│   ├── page.tsx        # Root page
│   └── [route]/        # Nested routes (static or dynamic)
│       ├── page.tsx
│       └── loading.tsx # Suspense fallback
├── components/         # UI components (dumb/presentational)
├── features/           # Smart components + feature-specific logic
├── lib/                # Utils, fetchers, actions (like "services")
├── styles/             # Global CSS, tailwind
├── public/             # Static assets
├── config/             # Tailwind, PostCSS, Next config
├── types/              # Shared types
└── package.json
```

# 2. The lib/ Folder: The Brain

Think of lib/ as your domain logic and services layer. Here’s what goes in:

- lib/actions/: Server Actions — new in React 19 / Next.js 15. These are async functions that mutate or fetch data on the server.

- lib/db/: Prisma, drizzle, SQL stuff? Goes here.

- lib/fetchers/: Shared data fetching functions (used by Server Components or RSC helpers).

- lib/utils.ts: Pure functions, helpers.

# 3. API Routes: Should You Use Them?

Short answer: **maybe not.**

With Server Actions, you don’t need to manually write API routes for form submits, mutations, or even fetching. 

Example:

```ts
'use server'

export async function savePost(data: FormData) {
  const title = data.get('title')
  // save to DB
}
```

**Then inside a component:**

```tsx
<form action={savePost}>
  <input name="title" />
  <button type="submit">Save</button>
</form>
```

**But! If you’re:**

- Handling webhooks

- Working with auth providers

- Exposing a JSON API

Then yeah, /app/api/route.ts is still the place.

# 4. Where Should You Fetch Data?

**For rendering pages:**

Use Server Components — default behavior in App Router.

Fetch data inside the component directly or use lib/fetchers.

```tsx
import { getPost } from '@/lib/fetchers/posts'

export default async function Page({ params }) {
  const post = await getPost(params.id)
  return <PostView post={post} />
}
```

**For client interactions:**

- Use React 19’s Server Actions.

- Or use useEffect for client-only data (non-critical stuff).

**TL;DR: Don’t fetch in useEffect unless you have to.**

# 5. Integration with Pages

- Default is Server Component.

- Wrap parts in <Suspense> or use loading.tsx for streaming.

- Use @server actions for mutations.

- Use @cache if you want revalidation helpers like revalidatePath.

# 6. Tailwind CSS 4 & TypeScript 5
Tailwind 4 is CSS-first: define tokens in globals.css, not tailwind.config.ts.

- TS 5 supports native decorators, better inference — keep types next to functions.

- Use @theme and CSS variables instead of over-customizing Tailwind in JS config.

# 7. Modern Dev Workflow Tips

- Use @/ aliases in tsconfig.json.

- Use loading.tsx over manual Suspense boundaries.

- Use useActionState or useFormStatus in React 19 to handle optimistic UI.

- Use Server Components by default. Wrap interactive bits in 'use client'.


