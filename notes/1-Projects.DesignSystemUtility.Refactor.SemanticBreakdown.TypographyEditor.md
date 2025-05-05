---
id: 9wp9wpshmxd1wpbnuts6ve4
title: TypographyEditor
desc: ''
updated: 1744604620865
created: 1744604620865

---

# 🧠 Semantic Breakdown of typography-editor.tsx

## 📦 Module: TypographyEditor

### 🔧 Helper Functions (→ typography-helpers.ts)

Function Name | Purpose
--------------|--------
getColorFromPalette() | Gets HEX color from color palette and shade
updateColorFromPalette() | Updates font color based on palette + shade

### 📁 Hooks & State Logic (→ useTypography.ts)

State Variable | Role
---------------|-----
fontSettings | Holds all typography settings for each category
activeCategory | Current active font tab (e.g. heading, body, caption)
uploadStatus | Tracks font upload status for each category
fontFaceCSS | Dynamically generated <style> block to load custom fonts
Hook | Description
useEffect() for CSS | Generates CSS rules from uploaded .ttf fonts
updateFontSettings() | Updates fontSettings record for the active category
handleFontUpload() | Converts uploaded .ttf file to usable font + injects into DOM


### 🧬 Font Settings Schema (→ typography-library.ts)

Constant Name | Use
--------------|----
defaultFontSettings | Holds base config for all 6 font categories
FontCategory (union type) | `"heading"

### 🎛 UI Components Used

Component | Purpose
----------|--------
Tabs, TabsList, TabsTrigger, TabsContent | Font category switcher
Slider | Font size, weight, line height, letter spacing
Input, Button | Upload field for .ttf files
Select family | Select font shade
Card, CardContent | Structure editor and preview layout
Label | All input labeling

### ✂️ Suggested Subcomponents

Subcomponent | File Name | Role
-------------|-----------|-----
FontTabPanel | FontTabPanel.tsx | A single tab view for settings of a specific font category
FontPreviewSection | FontPreview.tsx | Preview for heading, body, button, code, etc.
FontUploadField | FontUpload.tsx | Reusable upload control with icons & status

### 🧾 Dynamic CSS Logic

What it does | Suggested move
-------------|---------------
Dynamically generates and injects <style> with @font-face blocks from uploaded fonts | useTypography.ts or generateFontFaceCSS() helper

## ✅ Summary: What to Extract

### 🔁 Extract:

- typography-helpers.ts (color + palette utils)

- typography-library.ts (default font settings + types)

- useTypography.ts (all state, upload logic, CSS injection)

- FontTabPanel.tsx (tabs UI + inputs)

- FontPreview.tsx (UI for font display)

- FontUpload.tsx (upload UI + button + status icons)

### 🧱 Keep:

- TypographyEditor.tsx → as orchestration shell to import/render tabs and preview