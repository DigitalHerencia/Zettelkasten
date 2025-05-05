---
id: aedwvgy9vxz3r3wo21o4x0k
title: DecompositionPlan
desc: ''
updated: 1744604465127
created: 1744604465127
---

# 🧠 DesignSystemApp Decomposition Plan

## 📁 Proposed Structure

```pgsql
components/
├── app/
│   ├── DesignSystemApp.tsx             ← Wrapper only
│   ├── DesignSystemAppContent.tsx      ← Main shell
│   ├── NavigationMenu.tsx              ← DropdownMenu + Feature switching
│   ├── SaveButton.tsx                  ← Save logic with unsaved indicator
│   ├── FeatureView.tsx                 ← Dynamic switch for main features
│   ├── UnsavedWarningDialog.tsx        ← Dialog for unsaved changes
│   └── useFeatureManager.ts            ← All state/effects for active feature
```


### 🔁 What to Move Into Modules

| Logic/UI Element | Move to Component or Hook | Notes |
| --- | --- | --- |
| useState + useEffect for feature switching | useFeatureManager.ts | Manages: activeFeature, unsaved change logic, localStorage sync |
| Save Changes Button | SaveButton.tsx | Encapsulate: saveAllChanges, badge indicator, sessionStorage writes |
| Feature Switcher | NavigationMenu.tsx | Logic for feature switching and unsaved markers |
| Feature Render Logic | FeatureView.tsx | switch (activeFeature) {} → render components dynamically |
| QuickExportModal handler | DesignSystemAppContent.tsx | Leave it here unless it grows in complexity |
| Unsaved Warning Dialog | UnsavedWarningDialog.tsx | Controlled via props from useFeatureManager |

## 🧩 File Responsibilities

### ✅ DesignSystemApp.tsx

```tsx
export function DesignSystemApp() {
  return (
    <DesignSystemProvider>
      <DesignSystemAppContent />
    </DesignSystemProvider>
  )
}
```

### ✅ DesignSystemAppContent.tsx

- Imports useFeatureManager

- Includes 

  - <NavigationMenu /> 
  - <SaveButton /> 
  - <FeatureView /> 
  - <QuickExportModal />
  - <UnsavedWarningDialog />
  
  
### ✅ useFeatureManager.ts

```ts
export function useFeatureManager() {
  // activeFeature, unsaved state, localStorage sync
  return {
    activeFeature,
    handleFeatureChange,
    hasUnsavedChanges,
    confirmFeatureChange,
    cancelFeatureChange,
    quickExportOpen,
    handleQuickExport,
    exportData,
    ...
  }
}
```

### ✅ NavigationMenu.tsx

- Feature dropdown

- Triggers handleFeatureChange(feature)

### ✅ SaveButton.tsx

- Save changes

- Shows unsaved dot (hasUnsavedChanges)

### ✅ FeatureView.tsx

- Switch logic for rendering:

```tsx
switch (activeFeature) {
  case "colors": return <ColorPalette />;
  ...
}
```

### ✅ UnsavedWarningDialog.tsx

- Props: open, onStay, onDiscard, onSaveAndContinue

## ✅ Advantages of This Refactor

### Benefit	Impact
🔍 Improved readability	Each unit is <200 lines
🔄 Reusable logic	Navigation / Save / Dialogs can be reused site-wide
🧪 Easier testing	Unit test each piece independently
🧩 Feature-agnostic shell	Shell stays clean as features grow