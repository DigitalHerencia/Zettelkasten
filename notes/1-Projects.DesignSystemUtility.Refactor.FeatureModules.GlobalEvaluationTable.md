---
id: ff7fu5gech587xiznlvvv2m
title: GlobalEvaluationTable
desc: ''
updated: 1744604389772
created: 1744604389772
---

# 🧠 GLOBAL EVALUATION TABLE

File | Feature/Use | ✅ Keep | 🔁 Refactor/Move | ❌ Delete | 🆕 Create
-----|-------------|--------|------------------|----------|----------
design-system-context.tsx | Global State | ❌ Entire monolith | ✅ Decompose into feature contexts | ❌ This file entirely | context/[feature]-context.tsx per feature, + design-system-provider.tsx
components.ts | Components Library | ✅ componentDefinitions | 🔁 Export default + named categories | — | component-library-helpers.ts
colors.ts | Colors | ✅ Tailwind color data | 🔁 Move to lib/colors/colors-library.ts | — | color-helpers.ts, color-export.ts
typography.ts | Typography | ✅ Font size presets | 🔁 Move to lib/typography/typography-library.ts | — | typography-helpers.ts, typography-export.ts
fonts.ts | Typography/Fonts | ✅ Google fonts data | 🔁 Move to lib/fonts/font-library.ts | — | font-upload-utils.ts (if .ttf session-based loader)
icons.ts | Icons/Favicon/Logo | ✅ Icon metadata | 🔁 Move to lib/icons/icon-library.ts | — | icon-picker-utils.ts, favicon-export.ts, logo-helpers.ts
layouts.ts | Layout Editor | ✅ Generic template | 🔁 Move to lib/layouts/layout-library.ts | — | layout-editor-helpers.ts, layout-export.ts
db.ts | Not used yet | — | ❌ Not needed unless integrating Supabase | ✅ Delete for MVP | —
utils.ts | Global Utilities | ✅ Keep cn() | 🔁 Split reusable pure functions into local libs | ❌ Remove context-specifics | Create separate color, layout, component utility files

# 🗂️ REFACTORED FILE STRUCTURE (TARGET)

```css
context/
├── design-system-provider.tsx
├── color-context.tsx
├── typography-context.tsx
├── logo-context.tsx
├── favicon-context.tsx
├── layout-context.tsx
├── component-context.tsx
└── shared-types.ts

lib/
├── colors/
│   ├── colors-library.ts
│   ├── color-helpers.ts
│   └── color-export.ts
├── typography/
│   ├── typography-library.ts
│   ├── font-library.ts
│   ├── typography-helpers.ts
│   └── typography-export.ts
├── icons/
│   ├── icon-library.ts
│   ├── icon-picker-utils.ts
│   ├── favicon-export.ts
│   └── logo-helpers.ts
├── layouts/
│   ├── layout-library.ts
│   ├── layout-editor-helpers.ts
│   └── layout-export.ts
├── components/
│   ├── component-library.ts
│   ├── component-library-helpers.ts
│   └── component-export.ts
└── shared/
    ├── utils.ts (cn, copyToClipboard, etc.)
```