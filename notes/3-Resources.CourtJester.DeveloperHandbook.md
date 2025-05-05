---
id: mn3al7edqipx0kuujhbj3t0
title: DeveloperHandbook
desc: ''
updated: 1742704196109
created: 1742704189298
---
# Court Jester Developer Handbook 

## Directory Tree Overview

### /public

This folder contains static assets that are served directly by the web server.

#### Folder: fonts

- kings.woff2
A web font file (“Kings”) used for custom typography.

- jacquard-24-charted.woff2
A web font file (“Jacquard 24 Charted”) providing another custom typeface.

#### Files in /public

-joker-playing-card_u-l-q1llfru0.jpeg
A JPEG image asset—likely a design or decorative element in the UI.

- favicon.ico
The site’s favicon displayed in browser tabs.

- scale_black.png
A PNG image asset (black variant), possibly used as a logo or icon.

- scale_white.svg
An SVG version (white variant) of the scale image for scalable, resolution-independent display.

### Project Root

These files configure and govern the overall project behavior, build settings, and documentation.

- .env
Environment variables (database URI, secret keys, etc.) used by the application.

- .gitignore
Specifies files and directories that Git should ignore (e.g., node_modules, build artifacts).

- .hintrc
Configuration for HTML hinting/linting, including accessibility rules.

- components.json
JSON configuration defining UI component settings, aliases, and styling options.

-eslint.config.mjs
ESLint configuration file ensuring code quality and consistency.

- HELP.md
Documentation detailing features, button explanations, and usage instructions.

- middleware.ts
Next.js middleware handling request processing (such as authentication) before routing.

- monaco-environment.ts
Sets up the Monaco editor environment (used in-browser for code editing).

- next.config.ts
Next.js configuration for build options, experimental features, and optimizations.

- next-env.d.ts
TypeScript declaration file for Next.js environment types.

- package.json
Project manifest listing dependencies, scripts, and metadata.

- package-lock.json
Locked dependency tree to ensure reproducible builds.

- postcss.config.mjs
Configuration for PostCSS, commonly used with Tailwind CSS for styling.

- README.md
Overview of the project, setup instructions, and usage guidelines.

- tailwind.config.ts
Tailwind CSS configuration file defining themes, colors, and custom utilities.

- tsconfig.json
TypeScript compiler configuration specifying target language features and module resolution.

### /src

This directory contains the bulk of the source code—including type definitions, business logic, UI components, and API routes.

1. Type Definitions & Utilities

These files define TypeScript types, utility functions, and helper logic used throughout the project.

- api-types.ts
Defines API data structures such as motion templates and offender profiles.

- auth-types.ts
Contains type definitions for authentication sessions and user profiles.

- component-props.ts
Interfaces outlining the props for various UI components.

- models.ts
Mongoose model definitions for database entities (e.g., cases, motions).

- utility-types.ts
Additional type definitions for utility functions and component variations.

- api-utils.ts
General API helper functions (including standardized error responses).

- auth.ts
Handles JWT creation, verification, and token decoding for authentication.

- motion-templates.ts
Defines motion templates with placeholders and variables, and related helper functions.

- notifications.ts
Functions for managing and triggering notifications within the system.

- pdf-generator.ts
Uses pdfkit to generate PDF documents (such as motion documents).

- utils.ts
Common utility functions (e.g., merging CSS class names).

- validation.ts
Schema validations using Zod to ensure proper data formats.

- WithValidatedProps.tsx
A higher-order component that integrates prop validation using Zod.

- case-parser.ts
Parses raw textual case information into a structured data format.

- error-handler.ts
Centralized error handling logic for API routes.

- generate-motion-pdf.ts
Creates a PDF for a motion using motion data.

- generate-types-doc.ts
Script to generate documentation from TypeScript types.

- profile-parser.ts
Parses and structures offender profile data from text.

- connect.ts
Establishes the MongoDB connection using Mongoose.

2. Data Operations (Database Services)

Files managing data access and manipulation for various models.

- cases.ts
Functions to retrieve, create, and update legal case records.

- motions.ts
Handles creation and retrieval of motion records related to cases.

- offenders.ts
Manages offender data and related operations (e.g., fetching offender profiles).

- reminders.ts
Functions to create and manage reminder notifications.

- Case.ts
Mongoose schema and model for a legal case.

- Motion.ts
Mongoose schema and model for motions.

- Notification.ts
Mongoose schema/model for notifications.

- Offender.ts
Mongoose schema/model for offender information.

- Template.ts
Schema/model for document templates stored in the database.

3. Hooks & Global Utilities

Custom React hooks and utility files that enhance component functionality.

- use-mobile.ts
A custom hook to detect if the user is on a mobile device.

- use-toast.ts
Custom hook to trigger and manage toast notifications.

4. Main UI Components & Pages

Higher-level components that compose major sections of the application.

- confirmation-dialog.tsx

A modal dialog that asks the user to confirm an action.

- dashboard-skeleton.tsx
A placeholder skeleton UI displayed while dashboard data is loading.

- document-processing-tab.tsx
Component that allows users to process and parse document data (e.g., case details).

- floating-help-button.tsx
A fixed-position button that opens the help modal.

- help-button.tsx
A button that triggers the display of help information.

- help-menu-item.tsx
A menu item component for accessing help options.

- help-modal.tsx
A modal window providing help and support information.

- markdown-renderer.tsx
Renders Markdown content into HTML for display.

- motion-editor.tsx
Provides an interface for editing or creating motion documents.

- motion-history.tsx
Displays a list or history of motions related to a case.

- reminder-form.tsx
Form for creating or updating reminder entries.

- reminder-list.tsx
Lists all reminders with options for editing or deleting.

5. UI Elements (Atomic/Composite Components)

Reusable components forming the building blocks of the user interface.

- accordion.tsx
Collapsible accordion component for showing/hiding content.

- alert-dialog.tsx
Modal dialog specifically styled for alert messages.

- alert.tsx
A component to display inline alerts or notifications.

- aspect-ratio.tsx
Enforces a fixed aspect ratio on its children elements.

- avatar.tsx
Displays user avatars, typically in a rounded style.

- badge.tsx
A small label or badge used to indicate status or category.

- breadcrumb.tsx
Navigation aid that displays the current page’s hierarchy.

- button.tsx
A versatile button component with multiple variants.

- calendar.tsx
Date picker/calendar component for selecting dates.

- card.tsx
A container card used to group related UI content.

- carousel.tsx
A slider/carousel for displaying multiple items in a row.

- checkbox.tsx
A styled checkbox component.

- collapsible.tsx
Provides collapsible panels for content toggling.

- command.tsx
Implements a command palette for quick actions/navigation.

- context-menu.tsx
Context menu (typically on right-click) for additional options.

- dialog.tsx
A generic modal dialog component for various interactions.

- drawer.tsx
Side drawer component used for off-canvas menus or content.

- dropdown-menu.tsx
Dropdown menu component for lists of selectable options.

- form.tsx
A form wrapper component integrated with react-hook-form.

- hover-card.tsx
Displays additional information when hovering over an element.

- input-otp.tsx
Specialized input for entering one-time passcodes.

- input.tsx
Standard text input field.

- label.tsx
Label component used alongside form inputs.

- menubar.tsx
Horizontal navigation bar (menubar) component.

- navigation-menu.tsx
A multi-level navigation menu component.

- pagination.tsx
Controls for paginating long lists of items.

- popover.tsx
A small overlay that appears on demand to show extra content.

- progress.tsx
Displays a progress bar for ongoing operations.

- radio-group.tsx
Group of radio buttons for single-choice selections.

- resizable.tsx
Allows panels or elements to be resized by the user.

- scroll-area.tsx
Custom scrollable container for overflow content.

- select.tsx
Dropdown select input component with customizable options.

- separator.tsx
Visual divider used to separate UI sections.

- sheet.tsx
A bottom sheet component optimized for mobile interactions.

- sidebar.tsx
A sidebar navigation component for app-wide menu options.

- skeleton.tsx
Placeholder skeleton loader used during content loading.

- slider.tsx
A slider input component for selecting a range or value.

- sonner.tsx
Integrates with Sonner for advanced toast/notification displays.

- switch.tsx
Toggle switch component for binary options.

- table.tsx
Table component for structured data display.

- tabs.tsx
Tabbed interface for organizing content into sections.

- textarea.tsx
Multi-line text input component.

- toast.tsx
A component to display transient toast notifications.

- toaster.tsx
Container for managing and rendering toast notifications.

- toggle-group.tsx
Groups multiple toggle buttons together.

- toggle.tsx
A single toggle button component.

- tooltip.tsx
Displays contextual tooltips on hover.

6. Global Styles & Layout
Files that define the global look and structure of the app.

- globals.css
Global CSS rules and CSS variables (e.g., colors, typography).

- layout.tsx
The root layout component that sets up the overall page structure and includes common elements (like the toaster).

- page.tsx
A main page component (for instance, a homepage or case details page) that brings together various UI components.

- route.ts
Defines an API route (e.g., for deleting a case) and uses middleware for authentication.