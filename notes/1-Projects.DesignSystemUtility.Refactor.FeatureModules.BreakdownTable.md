---
id: i17r3lu4x8dqfoqkyxyrzdz
title: BreakdownTable
desc: ''
updated: 1744604184658
created: 1744604184658
---

# 📦 Feature Module Breakdown Table

| Feature             | Library File          | Helper Functions                     | Quick Export Functions              | Main Component(s)      | Secondary / Tertiary                           | Modal Component   | Page                        |
|---------------------|-----------------------|--------------------------------------|-------------------------------------|-------------------------|------------------------------------------------|-------------------|-----------------------------|
| 🎨 Color Palette    | lib/colors.ts         | color-helpers.ts (planned)           | color-export-functions.ts (planned) | ColorPalette           | CustomColorPicker, GradientColorPicker         | QuickExportModal  | color-palette.page.tsx      |
| 🔤 Typography       | lib/typography.ts     | typography-helpers.ts (planned)      | typography-export-functions.ts      | TypographyEditor       | TypographySettings, FontPreview, StylePreview  | QuickExportModal  | typography.page.tsx         |
| 🧬 Logo Editor      | lib/icons.ts          | logo-helpers.ts (planned)            | logo-export-functions.ts            | LogoEditor             | FontTab, TextTab, SVGTab                       | QuickExportModal  | logo-editor.page.tsx        |
| 🧩 Favicon Editor   | lib/icons.ts          | favicon-helpers.ts (planned)         | favicon-export-functions.ts         | FaviconEditor          | IconSelector, StyleAdjustments                 | QuickExportModal  | favicon-editor.page.tsx     |
| 🗂️ Layout Editor    | lib/layouts.ts        | layout-editor-helpers.ts             | layout-export-functions.ts (planned)| LayoutEditor           | GridControls, DivControls, ComponentControls   | QuickExportModal  | layout-editor.page.tsx      |
| 🧱 Component Library| lib/components.ts     | component-library-helpers.ts         | component-export-functions.ts       | ComponentLibrary       | BrowseComponentLibrary, AssignComponentLibrary | QuickExportModal  | component-library.page.tsx  |
| 📌 Notes            |                       |                                      |                                     |                       | All features use the shared QuickExportModal from components/quick-export-modal.tsx. |                   |                             |

- Helper & export functions are candidates for dedicated *.ts files under lib/ or helpers/.

- Pages are not currently separated in the codebase but are implied for feature modularization (e.g., color-palette.page.tsx).

The main component renders all logic in most current files (e.g., color-palette.tsx, typography-editor.tsx). These should be modularized into their sub-components per your refactor plan.