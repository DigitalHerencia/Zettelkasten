---
id: h9nbo1dqtxegh88mdaqu72a
title: LogoEditor
desc: ''
updated: 1744607037712
created: 1744607037712
---

# 🧠 Semantic Breakdown: LogoEditor

## 🧩 Primary Component

```tsx
export function LogoEditor() { ... }
```

### 🧠 Custom Types (Move to logo-types.ts)

Interface | Description
----------|------------
IconElement | An SVG-based icon placed on the canvas
TextElement | Text tied to the logo, can relate to an icon

### 🧰 Helper Functions (Move to logo-helpers.ts)

Function Name | Purpose
--------------|--------
calculateTextPosition() | Dynamically positions text relative to its linked icon
renderWrappedText() | Replaces /_/ token in text with inline icon rendering

### 🧬 Font Management (Move to logo-fonts.ts)

Function | Description
---------|------------
handleFontUpload() | Handles .ttf upload, creates @font-face, updates DOM
uploadedFonts state | Local state storing uploaded font names and URLs

### 🎨 SVG Upload (Move to logo-svg-upload.ts)

Function | Description
---------|------------
handleFileUpload() | Reads .svg as text and parses it into an icon element

### 🎛 State Variables (Move to useLogoEditor.ts)

Variable Name | Description
--------------|------------
iconElements | Array of placed icons
textElements | Array of text overlays
primaryText, secondaryText | Input buffer for each type of text
primaryTypography, secondaryTypography | Typography config for each text tier
canvasSize | Fixed canvas dimensions
activeElement/Type | Selected element and whether it's icon or text
dragStart, isDragging | For mouse drag & drop tracking

### 🔀 State/Action Functions (Move to useLogoEditor.ts)

Function Name	Description
addPrimaryTextToCanvas()	Adds primary text element
addSecondaryTextToCanvas()	Adds secondary text element
selectElement()	Activates selected element
removeElement()	Removes selected icon/text
updateIconElement()	Edits icon props (size, color, pos)
updateTextElement()	Edits text props (size, color, font, position)
handleMouseDown/Move/Up()	Drag & reposition logic

### 🧱 Suggested Subcomponents
Component | File Name | Role
----------|-----------|-----
CanvasPreview | LogoCanvas.tsx | Renders all positioned icons and text
FontUploadField | FontUploader.tsx | Upload logic + UI for .ttf fonts
SVGUploadField | SvgUploader.tsx | Upload SVG + display previews
TextControlPanel | TextEditorPanel.tsx | Inputs for primary/secondary text + colors
TypographyControlPanel | TypographyEditorPanel.tsx | Font size/weight sliders, color pickers
ElementControlPanel | ElementEditorPanel.tsx | Controls for selected element properties

### 🎛 UI Components Used

Library Element	Used For
Tabs, TabsTrigger, etc.	Editor panel navigation
Slider, Input, Select	Editing font properties and icon size
Button, Card, Label	Actions & layout wrappers

### 📤 Modular File Plan

File Name | Contents
----------|---------
logo-editor.tsx | Just imports + renders subcomponents
logo-types.ts | IconElement, TextElement, etc.
useLogoEditor.ts | State management + logic (replaces useState + handlers)
logo-helpers.ts | calculateTextPosition, renderWrappedText, utils
logo-fonts.ts | Font upload/injection logic
logo-svg-upload.ts | File upload + validation for SVG
LogoCanvas.tsx | Handles canvas + icon/text rendering
TextEditorPanel.tsx | Inputs for Primary / Secondary text
TypographyEditorPanel.tsx | Sliders + uploaders for typography
ElementEditorPanel.tsx | Logic for editing selected icon or text props

## ✅ Summary of Refactor

🧠 Extract logic-heavy chunks into useLogoEditor.ts
🎛 Componentize editor tabs for maintainability
🧩 Modularize upload logic and rendering
🔌 Clean top-level file to act only as container and orchestrator