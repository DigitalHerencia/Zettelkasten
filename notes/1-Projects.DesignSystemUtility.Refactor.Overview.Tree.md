---
id: m83mio8qg3r3nabwq7ykbdu
title: Tree
desc: ''
updated: 1744608675902
created: 1744608675902
---
design-system-generator/
├── app/                           # App router entrypoints
│   ├── layout.tsx
│   ├── page.tsx
│   ├── globals.css                # Move to styles/
│   └── api/
│       ├── fonts/
│       ├── icons/
│       └── upload-font/
│           └── route.ts
├── components/                   # Dumb, reusable UI components
│   ├── ui/
│   │   └── [core UI atoms/molecules]
│   ├── shared/                   # Composables: buttons, forms, toasts
│   │   ├── button.tsx
│   │   ├── toast.tsx
│   │   └── mode-toggle.tsx
│   └── layout/                   # Layout-oriented UI pieces
│       ├── app-sidebar.tsx
│       └── theme-provider.tsx
├── features/                     # Smart components with logic
│   ├── logo-editor/
│   │   └── index.tsx
│   ├── color-palette/
│   │   └── index.tsx
│   └── typography-editor/
│       └── index.tsx
├── hooks/                        # All React hooks
│   ├── use-toast.ts
│   ├── use-mobile.ts
│   └── use-local-storage.ts
├── lib/                          # Utilities and pure functions
│   ├── api/                      # Shared API utils
│   ├── constants/                # Color tokens, breakpoints, etc.
│   ├── utils.ts
│   ├── fonts.ts
│   └── db.ts
├── styles/
│   └── globals.css               # Tailwind + tokens here
├── config/                       # Configuration files
│   ├── tailwind.config.ts
│   ├── postcss.config.mjs
│   ├── next.config.mjs
│   └── tsconfig.json
├── public/
│   └── [assets/images/icons]
├── types/                        # Shared type definitions
│   └── index.ts
├── .gitignore
├── package.json
└── README.md
