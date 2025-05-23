---
id: 7m45bdkrwufspnhh62o5ep1
title: Tree
desc: ''
updated: 1736658121068
created: 1736647753212
---

# Project Directory Tree

Here's a **comprehensive directory tree** for the "Drama Drops" project using Next.js 15 with the App Router, React 19, Shadcn UI, Prisma, MongoDB, and Auth0, customized for Gadsden Panthers branding.
___

```
<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary dark:bg-gray-950"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between rounded-t-md h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none">plaintext</div><div class="sticky top-9 md:top-[5.75rem]"><div class="absolute bottom-0 right-2 flex h-9 items-center"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-sm"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy code</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre hljs language-plaintext">drama-drops/
├── public/                  # Static assets
│   ├── favicon.ico          # Favicon for the app
│   ├── logo.png             # Gadsden Panthers logo
│   ├── panthers-bg.jpg      # Background image for the branding
│   ├── robots.txt           # SEO settings
│   └── fonts/               # Custom fonts
│       ├── Inter-Regular.ttf
│       ├── Inter-Bold.ttf
│       └── ...
├── prisma/                  # Prisma schema and migrations
│   ├── schema.prisma        # Prisma ORM schema definition
│   └── migrations/          # Prisma migration files (generated)
│       ├── 20230101_init/
│       │   ├── migration.sql
│       └── ...
├── app/                     # Next.js App Router structure
│   ├── api/                 # API endpoints
│   │   ├── auth/
│   │   │   └── [...auth0]/  # Auth0 API routes for authentication
│   │   │       └── route.ts
│   │   ├── posts/           # Post-related APIs
│   │   │   ├── route.ts     # API endpoint to handle CRUD operations for posts
│   │   │   └── [id]/        # API for single post actions
│   │   │       └── route.ts
│   │   └── reactions/       # Reaction-related APIs
│   │       └── route.ts
│   ├── dashboard/           # Main app dashboard
│   │   ├── page.tsx         # Dashboard home page
│   │   ├── layout.tsx       # Dashboard-specific layout
│   │   └── components/      # Components for the dashboard
│   │       ├── PostCard.tsx # Component for displaying posts
│   │       ├── ReactionBar.tsx # Component for liking/reacting to posts
│   │       └── ...
│   ├── login/               # Login page
│   │   └── page.tsx         # Auth0 login page
│   ├── layout.tsx           # Global layout (e.g., navigation, footer)
│   ├── theme.ts             # Shadcn UI theme file customized for Gadsden Panthers
│   ├── page.tsx             # Landing page
│   └── styles/              # Global styles
│       └── globals.css      # TailwindCSS and Shadcn global styles
├── components/              # Shared components
│   ├── Navbar.tsx           # App navigation bar
│   ├── Footer.tsx           # App footer
│   ├── Button.tsx           # Shadcn Button component customization
│   └── ...
├── hooks/                   # Custom React hooks
│   ├── useAuth.ts           # Hook for Auth0 authentication
│   ├── usePosts.ts          # Hook for fetching and managing posts
│   └── useReactions.ts      # Hook for fetching and managing reactions
├── lib/                     # Utility libraries
│   ├── auth.ts              # Auth0 configuration helpers
│   ├── prisma.ts            # Prisma client instance
│   ├── fetcher.ts           # Utility for fetching API data
│   └── ...
├── pages/                   # Static Next.js pages (e.g., error pages)
│   ├── _app.tsx             # Global app configuration
│   ├── _document.tsx        # Document configuration (meta, fonts)
│   ├── 404.tsx              # Custom 404 error page
│   └── 500.tsx              # Custom 500 error page
├── tests/                   # Tests for components and pages
│   ├── components/          # Unit tests for components
│   │   ├── Navbar.test.tsx
│   │   ├── PostCard.test.tsx
│   │   └── ...
│   ├── pages/               # Tests for pages
│   │   ├── dashboard.test.tsx
│   │   └── ...
│   └── api/                 # Tests for API routes
│       ├── posts.test.ts
│       └── ...
├── .env                     # Environment variables (local development)
├── .env.production          # Environment variables (production)
├── next.config.js           # Next.js configuration
├── tailwind.config.js       # TailwindCSS configuration
├── postcss.config.js        # PostCSS configuration
├── tsconfig.json            # TypeScript configuration
├── package.json             # NPM scripts and dependencies
└── README.md                # Project documentation
</code></div></div>
```
