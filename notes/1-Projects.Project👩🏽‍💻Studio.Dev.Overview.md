---
id: qjccq82y0fr0sc7vzjarqz3
title: Overview
desc: ''
updated: 1742878329096
created: 1742878229867
---
# Project Studio Overview

## Features

1. Stack Builder: A guided wizard for selecting core technologies and preconfigured options.

2. Configuration Editor: An integrated code editor (using CodeMirror or Monaco) to edit essential files like package.json, .eslintrc.js, .prettierrc, and tailwind.config.js.

3. Boilerplate & Template Catalog: A searchable library for storing and previewing code snippets and file templates.

4. Directory Tree Planner: An interactive, drag‑and‑drop interface to design and export the project’s file structure.

5. Documentation Hub: A curated section linking to Next.js, React, Tailwind, and other docs.

6. UI Component Selector: A catalog for browsing and selecting prebuilt ShadCN UI components.

7. Codebase Visualization & Data Model Diagram: 

- Functionality to ingest a Next.js project (via ZIP upload or GitHub URL), parse its AST to generate an interactive dependency graph (or container diagram) and extract model definitions (e.g., Mongoose schemas) to produce an ERD/UML diagram. Nodes in these diagrams should be clickable—displaying relevant code or metadata—and support zoom/pan and filtering.

## Structure

The backend will use Next.js API routes and server actions (located in a modular lib folder) for all CRUD operations, with persistent storage in MongoDB and user-specific workspaces secured by Clerk authentication. The app should follow the conceptual file structure outlined below:

```plaintext
project-studio/
├── app/
│   ├── dashboard/                // Main dashboard with project overview and navigation
│   ├── stack-builder/           // Wizard UI for defining the tech stack
│   ├── config-editor/           // Code editor for configuration files
│   ├── directory-planner/       // Drag-and-drop interface for directory tree design
│   ├── template-catalog/        // Boilerplate/template catalog UI
│   ├── docs-hub/                // Documentation links and resources
│   ├── ui-components/           // ShadCN UI component selector
│   ├── diagrams/
│   │   └── [projectId]/page.tsx  // Page to display codebase and data model diagrams
│   ├── layout.tsx                // Global layout (includes ClerkProvider, theme providers)
│   └── global.css                // Global styles (with Tailwind directives)
├── lib/
│   ├── actions/                 // Server actions for saving projects, templates, etc.
│   └── db/                      // MongoDB connection logic using Mongoose
├── models/                      // Data models (e.g., Project, Template)
├── utils/                       // Helper functions, Zod schemas, etc.
├── .eslintrc.js
├── .prettierrc
├── next.config.js
├── package.json
├── tsconfig.json
└── tailwind.config.js

```

## UX

When the user uploads or provides a GitHub URL for a Next.js project, the app should:

1. Store (or clone) the project code.

2. Run a server-side analysis that:

3. Walks the file system and uses an AST parser (via the TypeScript compiler API or Babel) to extract import/export relationships, Next.js–specific files (pages, layouts, server actions), and any model definitions (e.g., Mongoose schemas).

4. Transforms this information into a JSON structure representing a dependency graph and a separate data model graph.

5. On the client side, render interactive diagrams using a library such as react-flow, D3.js, or Mermaid (with zoom, pan, expand/collapse, and click-to-view–code features).