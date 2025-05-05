---
id: ik0hzj2vgeaadqcm4hq3eae
title: 3-Structure
desc: ''
updated: 1742524346605
created: 1742523935880
---
## 3. Structure of Teams and 

### Workgroups

We mirror the project’s folder structure as follows:

#### A. App Team (Frontend Pages & API Routes)

##### Workgroups:

- Pages Workgroup: Responsible for page components (e.g. app/[route]/page.tsx).
  - Roles: Frontend Page Prompter, Frontend Page Worker, Frontend Page QA
- Layouts Workgroup: For layouts and global page structure.
  - Roles: Layout Prompter, Layout Worker, Layout QA
- API Routes Workgroup: For Next.js API endpoints (e.g. app/api/route.ts).
  - Roles: API Prompter, API Worker, API QA

#### B. Components Team (Reusable UI Components)

##### Workgroups:

- UI Components Workgroup: For reusable elements (e.g. buttons, forms, cards).
  - Roles: Component Prompter, Component Worker, Component QA

#### C. Lib Team (Backend Logic & Shared Code)

##### Workgroups:

- Models Workgroup: For database schema and models (e.g. Mongoose models).
  - Roles: Model Prompter, Model Worker, Model QA
- Utils Workgroup: For utility functions and business logic helpers.
  - Roles: Utils Prompter, Utils Worker, Utils QA
- Types Workgroup: For TypeScript definitions and interfaces.
  - Roles: Types Prompter, Types Worker, Types QA
- Auth Workgroup: For Clerk integration, ABAC, and middleware.
  - Roles: Auth Prompter, Auth Worker, Auth QA

#### D. CI/CD & Deployment Team

##### Workgroups:

- Pipeline Workgroup: For creating GitHub Actions workflows and build scripts.
  - Roles: CI Prompter, CI Worker, CI QA
- Deployment Workgroup: For Vercel configuration and deployment settings.
  - Roles: Deploy Prompter, Deploy Worker, Deploy QA

####  E. Type System Team (Cross-Cutting)

##### Workgroup:

- Type Checker Workgroup: Enforces strict TypeScript usage across the project.
  - Roles: Type Checker Prompter, Type Checker Worker, Type Checker QA