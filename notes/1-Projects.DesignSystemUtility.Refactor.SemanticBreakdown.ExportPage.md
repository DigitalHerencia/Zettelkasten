---
id: w1gp2uewipd6zqqifqy4i7p
title: ExportPag
desc: ''
updated: 1744607192802
created: 1744607192802
---

# 🧠 Semantic Breakdown: ExportPanel

## 🔁 Helper Functions (→ export-helpers.ts)

Function Name | Purpose
--------------|--------
generateGlobalsCss() | Creates CSS with Tailwind layers and injected font/color variables
generateTailwindConfig() | Builds tailwind.config.ts with full theme extensions
generateComponentsJson() | Returns components.json for ShadCN setup
generateLayoutTsx() | Generates app layout shell (with favicon/logo)
generateLayoutModuleCss() | Outputs per-layout responsive .module.css styles
generateComponentTsx() | Returns compiled component JSX string per definition
generateFileList() | Collects all files to include in the export ZIP
copyToClipboard() | Copies preview content to clipboard with feedback

## 🧬 Hook State Logic (→ useExportPanel.ts)

State Key | Description
----------|------------
exportSettings | Contains filename, path, comment toggles
isExporting | Toggles export progress loader
exportProgress | Simulates progress meter for UX
copied, exportComplete | Visual feedback flags
activeTab | Switch between Preview and Structure views
Hook | Notes
useDesignSystem() | Pulls state, layouts, selected components, fonts, etc.

## 🧱 Subcomponents (Suggested Extraction)

Component Name | File | Description
---------------|------|------------
ExportSettingsPanel | ExportSettingsPanel.tsx | Handles name, path, options checkboxes
ExportSelectedComponents | ExportSelected.tsx | Badge-style component export summary
ExportButtonWithProgress | ExportButton.tsx | Handles async simulation + completion message
ExportPreviewPanel | ExportPreview.tsx | File viewer tab: file selector, syntax preview, copy button
ExportStructurePanel | ExportStructure.tsx | Renders folder/file tree + Next.js export notes

## 📁 Suggested Folder Structure

```cpp
features/
└── export/
    ├── ExportPanel.tsx
    ├── useExportPanel.ts
    ├── export-helpers.ts
    ├── ExportSettingsPanel.tsx
    ├── ExportSelected.tsx
    ├── ExportButton.tsx
    ├── ExportPreview.tsx
    ├── ExportStructure.tsx
```

## ✅ What to Keep in ExportPanel.tsx

- <Tabs> layout and shell

- Composition of all extracted subcomponents

- Orchestration of preview tab and structure tab render

## 🔧 Additional Notes

**The simulated ZIP export process is UI-only. You may later replace it with real file packaging using:**

- jszip

- file-saver