---
id: hzzy2b7pgkusm4rprowtvgf
title: Promp
desc: ''
updated: 1742878939986
created: 1742878919007
---
# Prompt

Build a Vercel-optimized Next.js 15 app called "Project Studio" with the following features and functionality, using React 19, TypeScript 5, Tailwind CSS 4, and ShadCN UI 2. Use MongoDB (via Mongoose), Zod, ESLint, Prettier, and integrate Clerk for authentication.

The app should provide an interactive platform where junior developers can build their project blueprint step by step:

1. **Stack Builder:**  
   - A guided wizard for selecting core technologies and configuration options (Next.js, React, TypeScript, Tailwind, ShadCN UI, MongoDB/Mongoose, Zod, ESLint, Prettier, Clerk).
  
2. **Configuration Editor:**  
   - An integrated code editor (using CodeMirror or Monaco) for creating and editing configuration files such as package.json, .eslintrc.js, .prettierrc, and tailwind.config.js.  
   - Provide live syntax highlighting and linting feedback.

3. **Boilerplate & Template Catalog:**  
   - A searchable library for organizing, previewing, and saving boilerplate code snippets and file templates.

4. **Directory Tree Planner:**  
   - An intuitive, drag-and-drop interface to design the project’s file structure.  
   - Allow exporting the structure as JSON or plain text.

5. **Documentation Hub:**  
   - A section that aggregates relevant documentation and learning resources for Next.js, React, Tailwind CSS, and more.

6. **UI Component Selector:**  
   - A curated interface to browse and select prebuilt ShadCN UI components with usage examples and documentation links.

7. **Codebase Visualization & Data Model Diagram:**  
   - On the server, analyze the provided project by:
     - Recursively scanning the project folder (ignoring node_modules) to build a dependency graph using AST parsing (with the TypeScript compiler API or Babel).  
     - Identifying Next.js–specific artifacts (pages, layouts, server actions) and model definitions (e.g., Mongoose schemas) to generate a data model diagram (ERD/UML).
   - Transform the extracted data into JSON graph structures.
   - Render interactive diagrams on the frontend using libraries like react-flow, D3.js, or Mermaid.  
     - Diagrams should support zoom, pan, expand/collapse nodes, and clicking on a node to view the corresponding code snippet.
   - Provide functionality for users to upload a ZIP file or enter a GitHub repo URL of an existing Next.js project.  

8. **Backend & API:**  
   - Implement Next.js API routes and server actions (located in a modular lib folder) to handle project uploads, AST parsing, diagram generation, and saving user customizations.  

9. **Overall Architecture & File Structure:**  
    - Organize the project into modules: dashboard, stack-builder, config-editor, directory-planner, template-catalog, docs-hub, ui-components, and diagrams, following a modular file structure.  

Please generate all necessary Next.js files (pages, components, API routes, server actions, and configuration files) to create a polished, production-ready "Project Studio" app. Ensure the code follows best practices with TypeScript, ESLint, and Prettier, and that the UI is modern and intuitive for junior developers.