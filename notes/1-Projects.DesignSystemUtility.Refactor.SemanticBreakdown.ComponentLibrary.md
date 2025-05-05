---
id: 7lbfgtuq77vsmg84dvrhw9z
title: ComponentLibrary
desc: ''
updated: 1744607163291
created: 1744607163291
---

# 🧠 Semantic Breakdown: ComponentLibrary

## 📦 Primary Component

```tsx
export function ComponentLibrary() { ... }
```

## 🔁 Helper Functions → component-library-helpers.ts

Function Name | Description
--------------|------------
getColorFromPalette() | Retrieves HEX value from color palette + shade
toggleComponentSelection() | Adds/removes components from export selection
handleComponentSelection() | Updates componentId of a layout item
filteredComponents() | Filters by category and search term
getUniqueCategories() | Extracts all distinct categories from componentDefinitions

## 🧬 Hook / Logic Split → useComponentLibrary.ts

State Key | Description
----------|------------
searchTerm | Component name search input
selectedCategory | Category filter
activeLayout | Currently selected layout for assigning components
activeComponent | Selected layout item to which a component is being assigned
selectedComponentType | The componentId of selected layout item
Derived Data | Source
allComponentItems | All layout items across all layouts
layoutComponentItems | Items from the currently active layout
filteredComponents | Result of category + search filter
categories | All unique component categories

## 🧱 UI Subcomponents

Component Name | File | Responsibility
---------------|------|---------------
ComponentSearchPanel | ComponentSearchPanel.tsx | Search input, category filters
ComponentGrid | ComponentGrid.tsx | Render filteredComponents cards
ComponentAssignPanel | ComponentAssignPanel.tsx | Right panel of assign tab with select dropdown + preview
ComponentLayoutList | ComponentLayoutList.tsx | Renders layout component buttons (on the left panel)
CustomizationAccordion | CustomizationAccordion.tsx | Accordion with color and typography controls
ComponentPreviewCard | ComponentPreviewCard.tsx | Individual UI card for component in grid

## 📤 Export Candidate → component-export.ts

Utility | Description
--------|------------
getSelectedComponents() | Return only the checked component definitions for export
generateComponentExportJSON() | Produces structured export data

## 📁 Refactored File Structure

```cpp
features/
└── component-library/
    ├── ComponentLibrary.tsx
    ├── useComponentLibrary.ts
    ├── component-library-helpers.ts
    ├── component-export.ts
    ├── ComponentSearchPanel.tsx
    ├── ComponentGrid.tsx
    ├── ComponentPreviewCard.tsx
    ├── ComponentLayoutList.tsx
    ├── ComponentAssignPanel.tsx
    ├── CustomizationAccordion.tsx
```

## ✅ What Stays in ComponentLibrary.tsx

- <Tabs> UI shell

**Render imports:**

- <ComponentSearchPanel />

- <ComponentGrid />

- <ComponentAssignPanel />

**State can be centralized in useComponentLibrary()**

## 🎛 UI Components Used (ShadCN UI)

- Tabs, Select, Button, Input, Card, Checkbox, Badge, Accordion

- Minimal custom styling required — can be handled via Tailwind and class variants

## ✅ Summary of Refactor

### Category	Action

🧠 Logic/State	Move all useState + useEffect logic into useComponentLibrary.ts
🧰 Helper Functions	Extract getColorFromPalette, filtering logic to component-library-helpers.ts
🧱 UI Panels	Componentize tabs, grid, assign panel, and card previews
📤 Export Handling	Build component-export.ts to support future export actions