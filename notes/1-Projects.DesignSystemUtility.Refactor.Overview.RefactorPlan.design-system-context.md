---
id: 7m2g0lg0fc5fvf5yazo0bx1
title: design-system-cotext
desc: ''
updated: 1744604302370
created: 1744604302370
---

# 🧠 Refactor Plan: design-system-context.tsx

## 🎯 Goals

Split by feature: 

- color
- typography
- logo
- favicon
- layout
- components.

**Preserve a global provider:** so consuming components don’t need to change.

**Ensure modularity:** each feature manages its own slice of state, default values, and update logic.

**Improve maintainability:** reduce merge conflicts, improve unit test coverage, isolate unsaved state tracking.

## 📁 Folder-Based Modular Context System
```css
context/
│
├── design-system-provider.tsx         ← Root aggregator
│
├── color-context.tsx                  ← 🎨 Color state and updater
├── typography-context.tsx             ← 🔤 Typography settings
├── logo-context.tsx                   ← 🧬 Logo SVG + elements
├── favicon-context.tsx                ← 🧩 Favicon settings
├── layout-context.tsx                 ← 🗂️ Grid, divs, componentItems
├── component-context.tsx              ← 🧱 Selected components, mappings
│
└── shared-types.ts                    ← Shared state types & constants
```

## 🧩 Breakdown by Module

### ✅ color-context.tsx

- selectedColorPalette

- customColors

- unsavedColorChanges

- updateColorPalette()

- updateCustomColors()

- getColorByShade()

### ✅ typography-context.tsx

- fonts

- unsavedFontChanges

- updateFonts()

### ✅ logo-context.tsx

- logo

- unsavedLogoChanges

- updateLogo()

### ✅ favicon-context.tsx

- favicon

- unsavedFaviconChanges

- updateFavicon()

### ✅ layout-context.tsx

- layouts

- unsavedLayoutChanges

- updateLayout()

- addLayout()

- removeLayout()

- updateDivElement()

- addDivElement()

- removeDivElement()

- updateComponentItem()

- addComponentItem()

- removeComponentItem()

### ✅ component-context.tsx

- selectedComponents

- unsavedComponentChanges

- updateSelectedComponents()

## 🔄 design-system-provider.tsx

This new file becomes a wrapper provider that aggregates all feature contexts into a single hook:

```tsx
export const DesignSystemProvider = ({ children }: { children: React.ReactNode }) => (
  <ColorProvider>
    <TypographyProvider>
      <LogoProvider>
        <FaviconProvider>
          <LayoutProvider>
            <ComponentProvider>
              {children}
            </ComponentProvider>
          </LayoutProvider>
        </FaviconProvider>
      </LogoProvider>
    </TypographyProvider>
  </ColorProvider>
);
```

**And expose a unified hook like:**

```tsx
export const useDesignSystem = () => ({
  ...useColorContext(),
  ...useTypographyContext(),
  ...useLogoContext(),
  ...useFaviconContext(),
  ...useLayoutContext(),
  ...useComponentContext(),
});
```

## 📦 Export Handling (Optional Refactor)

Move all getExportData(feature) logic into a utility module:

```cpp
lib/
└── export-engine/
    ├── colors-export.ts
    ├── typography-export.ts
    ├── logo-export.ts
    ├── favicon-export.ts
    ├── layout-export.ts
    └── components-export.ts
```

Let each feature own its export format, and centralize logic for .zip, .json, .css, .ico, or .svg compilation.

### ✅ Benefits of This Refactor

🔓 Unlocks better scalability: future features (animations, interactions, metadata) can be added with isolated files.

🧪 Improves testability: you can test color updates without dealing with typography.

🚀 Enables SSR or persistence migration: can move each state slice to IndexedDB, localStorage, or Supabase independently.

📉 Minimizes conflicts: avoids the pain of multiple devs touching the same 800-line file.