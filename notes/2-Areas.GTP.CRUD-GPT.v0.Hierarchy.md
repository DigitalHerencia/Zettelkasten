---
id: rlf5xts5xe83xondi8f43vt
title: Hierarchy
desc: ''
updated: 1742536373723
created: 1742536373723
---
## Hierarchical Team Structure

To organize these workgroups, we adopt a hierarchical **team-of-teams** structure that mirrors a standard Next.js project layout. In a Next.js 15 application (using the App Router), you typically have high-level folders like `app/`, `components/`, `lib/`, etc., each with specific subfolders or file conventions. We use an analogous setup for our GPT teams:

- **App Team:** Responsible for the overall application structure and user-facing pages. This team corresponds to the Next.js `app/` directory which contains route definitions, layouts, and UI pages​. Within the App Team, we have workgroups such as **Pages**, **Layouts**, and **API Routes**. For example, a “Page” GPT (set of Prompter/Worker/QA) handles the creation of a new page (`page.tsx`) given a route and design spec, while a “Layout” GPT set ensures consistent layout components for sections of the app. The **API** workgroup here covers any `/app/api` route endpoints (since Next.js API routes might live under the app directory in Next 15). Essentially, the App Team orchestrates front-end page delivery and integrates with backend endpoints as needed.
- **Components Team:** This corresponds to the reusable UI components library (the `components/` folder). Its GPT workgroup is focused on **UI Components** – creating and styling React components using ShadCN UI and Tailwind CSS. For instance, if the design calls for a `<Button>` or a complex widget, the Components Team’s GPTs will generate those JSX/TSX files. They follow the design system guidelines (e.g. using ShadCN’s accessible component patterns and Tailwind utility classes) so that the style is consistent. Having a dedicated Components team ensures UI elements are developed with reusability and proper UX in mind, separate from page-specific logic.
- **Lib Team:** This reflects the `lib/` (or sometimes `utils/` and `models/`) directories where backend logic and shared utilities reside​. The Lib Team encompasses workgroups like **Models**, **Utils**, and **Types**. The **Models** GPTs handle data schema definitions and database integration (e.g. defining Mongoose models for MongoDB, including schema fields and validation rules). The **Utils** GPTs cover business logic helpers or server-side utilities (for example, functions for calculations, formatting, etc., that might go in a `lib/utils.ts` file). The **Types** GPT focuses on TypeScript type definitions and interfaces (ensuring that shared types are declared and used uniformly across frontend and backend, supporting strong typing throughout the codebase). There might also be an **Auth** workgroup here (for authentication and authorization logic, such as generating an Express/Next middleware for ABAC rules). By segmenting these, the Lib team ensures the backend logic and cross-cutting concerns are well-structured and adhere to best practices (for instance, the Auth GPT would implement an attribute-based access control middleware, evaluating user and resource attributes against policies​).

- **CI/CD & Deployment Team:** This team handles the DevOps side (not a folder in the app, but an important part of the project). Its GPTs manage configuration files and deployment scripts. One workgroup might create a **CI Pipeline** (for example, a GitHub Actions YAML that runs tests and lints, or a Vercel configuration file). Another might handle **Deployment** specifics (like provisioning a `vercel.json` or Dockerfile, or documentation for how to perform rollbacks). They encapsulate knowledge of Git integration, testing frameworks, and Vercel deployment steps. For example, the CI Prompter might ask for project-specific build and test commands, the worker GPT writes a YAML with those steps, and the QA GPT verifies that the pipeline will run successfully (catching syntax errors or missing environment variables).
- **Type System Management Team:** While type enforcement is a theme throughout (especially via the Types workgroup in Lib), we allocate a team to ensure **TypeScript correctness** across all outputs. This can be a specialized QA agent or set of agents that perform static analysis on the generated code. In practice, this might mean after all code is generated, a Type Checker GPT reviews the combined codebase (or type definitions) to identify any type mismatches or implicit `any` usage and then suggests fixes. This team enforces a strict TypeScript configuration (for example, `tsconfig.json` with noUncheckedIndexedAccess, strict null checks, etc.) and ensures each part of the project conforms to it. The benefit is that many errors are caught early in the GPT stage, and the final code will compile cleanly with strong typing. (In the future, this could even be connected to run `tsc` in a sandbox and feed errors back to a GPT for automatic correction.)

All these teams and workgroups are discrete, but they pass **formatted outputs as inputs to the next stage** in a pipeline. The overall hierarchy can be visualized as an organization chart of AI agents, roughly analogous to a real engineering team:

- **Project (ChatGPT System)**
    - **App Team**(Frontend Pages & Routes)
        - Pages Workgroup – *Page Prompter GPT, Page Worker GPT, Page QA GPT*
        - Layouts Workgroup – *Layout Prompter, Worker, QA*
        - API Routes Workgroup – *API Prompter, Worker, QA*
    - **Components Team**(UI Library)
        - UI Components Workgroup – *Component Prompter, Worker, QA*
    - **Lib Team**(Backend Logic)
        - Models Workgroup – *Data Model Prompter, Worker, QA*
        - Utils Workgroup – *Utility Function Prompter, Worker, QA*
        - Types Workgroup – *Type Definitions Prompter, Worker, QA*
    - **CI/CD Team**(DevOps)
        - Pipeline Workgroup – *CI Prompter, Worker, QA*
        - Deployment Workgroup – *Deploy Prompter, Worker, QA*
    - **Type System Team**(Cross-cutting)
        - Type Checker Workgroup – *Typescript Enforcement GPTs (prompter & checker)*

Each item in this hierarchy represents either a team (bold) or a specific workgroup (with the GPT roles in italic). The **flow of information** typically goes from top to bottom: e.g. the Project lead (user) assigns a feature to the App Team; within App, the Page workgroup is engaged and produces outputs; the Page workgroup might request help from the Components team if a new UI element is needed; similarly, it might interface with the Lib team if a new API or model is required for that page. All communication remains in structured text form passed via the user, maintaining the manual but organized workflow.

This hierarchical setup closely mirrors how a Next.js codebase is structured and how a cross-functional dev team might collaborate. It ensures that **nothing falls through the cracks** – each directory or concern in the project has an assigned GPT (or group of GPTs) “responsible” for it, complete with checks and balances. By following the Next.js 15 project conventions (app, components, lib, etc.), the AI-generated output will be easier for human developers to understand and pick up, since the files and folders will be where you expect them and follow familiar patterns​.

Moreover, the teams approach makes it scalable: if the project grows in complexity, you can add another workgroup (say for a new microservice or a new domain) without disrupting others, much like adding a new department to an organization.

[wisp.blog](https://www.wisp.blog/blog/the-ultimate-guide-to-organizing-your-nextjs-15-project-structure#:~:text=Let%27s%20start%20with%20the%20foundation,organized%20Next.js%2015%20project)

[osohq.com](https://www.osohq.com/post/implementing-attribute-based-access-control-abac-in-node-js-with-oso#:~:text=,grained%20and%20flexible%20access)
