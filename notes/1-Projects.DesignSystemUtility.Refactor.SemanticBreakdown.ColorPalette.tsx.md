---
id: dc7onvio0psq164219naslu
title: tsx
desc: ''
updated: 1744604539444
created: 1744604539444
---

# 🧠 Semantic Breakdown of color-palette.tsx

## 📦 Module: ColorPalette (Main Component)

### 🔧 Helper Functions (Move to color-helpers.ts)

| Function Name |	Purpose |
| --- | --- | 
| hexToRgb(hex)	| Converts HEX color to RGB format |
| rgbToHex(r,g,b) |	Converts RGB values to HEX string |
| mix(c1, c2, w) |	Mixes two RGB colors with a weight ratio | 
| mixToHex(...) |	Composes mix and rgbToHex to get a mixed HEX value |
| generateColorPalette(baseColor)	| Generates Tailwind-style palette from base color |

### 🎛️ UI Components Used

|UI Element	| Purpose |
| --- | --- | 
Card, CardContent	| Content containers
Tabs, TabsList, TabsTrigger, TabsContent	| For selecting predefined palettes vs custom
Input	Color | picker input
Button	|  UI triggers (custom select, gradient modal, copy, etc.)
Checkbox	| Toggle gradient mode
Slider |	Angle control for linear gradients
Select | family	UI controls for palette name, gradient | shade selection
Dialog, DialogContent, etc.	| Modal for gradient settings
Copy, Check, Droplet | Icons for interactivity

### 🧬 Context API 
|Hook Used	| Usage |
| --- | ---|
useDesignSystem()	| Accesses: state, updateColorPalette, updateCustomColors

### 🧠 Component State (Move to useColorPalette.ts)

| State  Variable	| Description |
| ---  | --- |
selectedPalette	| Current color palette selected (including "custom")
customColor |	HEX base color for custom palette
customPalette	| Generated palette from customColor
copied |	Tracks copied HEX for visual feedback
gradientEnabled	| Boolean flag for enabling gradient preview
gradientType	| "linear" or "radial"
gradientAngle	| Numeric value (0–360°)
gradientStartShade	| Shade for gradient start
gradientEndShade	| Shade for gradient end
gradientModalOpen |	Boolean to toggle modal open


### 📤 Side Effects (Keep in ColorPalette or useColorPalette.ts)

| Hook	| Purpose |
| --- | --- | 
useEffect(...)	| Re-generate palette when customColor changes
useEffect(...)	| Sync selected palette to sessionStorage, update default shades
useEffect(...)	| Update customColors in context if customPalette changes

### ✂️ Candidates for Componentization

| Subcomponent	| Suggested File Name	| Role
| --- | --- | --- |
ColorSwatchGrid	| ColorSwatchGrid.tsx |	Renders grid of 11 swatches per palette
CustomColorPicker |	CustomColorPicker.tsx	| Picker + icon buttons for HEX, checkmark, and gradient modal
ColorPaletteTabs	| ColorPaletteTabs.tsx |	Tab layout for switching palettes
LightModePreview	| ColorPreviewLight.tsx |	Button and text color preview with white background
DarkModePreview |	ColorPreviewDark.tsx	| Same as above, but with custom gradient/dark background
GradientSettingsModal	| GradientSettingsModal.tsx |	All dialog-based controls for gradient configuration

## ✅ Summary of What to Extract

### 🔌 Create:

- color-helpers.ts

- useColorPalette.ts

- ColorSwatchGrid.tsx

- ColorPreviewLight.tsx

- ColorPreviewDark.tsx

- CustomColorPicker.tsx

- ColorPaletteTabs.tsx

- GradientSettingsModal.tsx

### 🔁 Keep in ColorPalette.tsx:

- High-level layout shell

- State orchestration (or move to useColorPalette)

- Import and glue subcomponents