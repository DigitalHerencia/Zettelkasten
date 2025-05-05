---
id: o440jnipmsacqd7t480v6i3
title: ComponentLibrary
desc: ''
updated: 1744604072031
created: 1744604072031
---

# Component Library Refactor Plan

## 1. Library File (e.g., component_library.ts)

### Purpose

Store reusable data related to the component system.

#### Contents

* Import and export componentDefinitions from components.ts.
* Optionally include categories, default filters, and sample configurations for initialization.

### 2. Helper Functions File (e.g., component_library_helpers.ts)

#### Purpose

Encapsulate non-UI logic for filtering, searching, and palette lookups.

#### Functions to Include

* `filterComponents(searchTerm: string, category: string, definitions: Component[]): Returns the filtered components.`
* `getColorFromPalette(palette: string, shade: number): string`: Already used inline — extract to this file.
* `getLayoutComponentItems(layoutId): Safely retrieves and formats component items from layouts.`
* Any logic currently embedded in hooks or handlers that can be abstracted for reuse.

### 3. Sub-Components

#### a) BrowseComponentLibrary

##### Purpose

Handles the browse tab. Renders search, filters, and preview grid.

##### Features

* Uses componentDefinitions and the helper filter function.
* Displays preview cards with select checkboxes for exporting.

#### b) AssignComponentLibrary

##### Purpose

Handles the assign tab. Renders layout/component assignment UI.

##### Features

* Dropdown to select a layout.
* Interactive list of layout component items.
* Assign a component with a select dropdown, preview area, and customization accordion.

#### c) ComponentItemPreview

##### Purpose

Reusable card component showing the live preview, category, and checkbox.

### 4. Modal Component (optional)

Optional if you want to allow exporting selected components or managing batch assignments via modal.

* Component: `ComponentLibraryExportModal.tsx`
* Functions File: `component_library_modal_functions.ts`
* Functions:
	+ Build selected export list.
	+ Package export data (HTML, JSON, or JSX).
	+ Open, close, and trigger export actions.

### 5. Page Integration (e.g., component-library.page.tsx)

#### Purpose

Renders the top-level tabs, integrates Browse and Assign components, and manages state via context.

#### Features

* Tabs: browse, assign.
* Includes logic for current layout and selected component management.
* Modal trigger if applicable.

### Bonus: State Management

Since this already uses `useDesignSystem`, the only requirement is to keep prop drilling minimal between the subcomponents. Use the hook directly inside each module where needed.