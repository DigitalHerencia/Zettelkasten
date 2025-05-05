---
id: sv1cdc7fuy6uxk1n31usv34
title: 2-Tech-Stacks
desc: ''
updated: 1742523739606
created: 1742523609270
---
## 2. Tech Stack Segments
The tech stack is segmented into four major areas:

### Frontend:

- Framework & Routing: Next.js 15 (App Router with Advanced Routing)
- UI Libraries: React 19, ShadCN UI, Tailwind CSS, Lucide Icons, ShadCN Charts
- State Management & Data Fetching: Redux Toolkit/RTK Query, Mapbox integration

### Backend:

- API & Business Logic: Next.js API Routes, custom business logic in /app/api
-  Authentication & Authorization: Clerk authentication, ABAC middleware
- Database: MongoDB with Mongoose for schema-based ORM

### CI/CD & Deployment:

- Hosting: Vercel (Blob storage and Fluid Compute)
- Version Control & Automation: GitHub, GitHub Actions workflows
- Code Quality Tools: ESLint, Prettier

### Type System & Utilities:

- TypeScript Enforcement: Strongly typed interfaces and schemas (in lib/types)
- Shared Utilities: Conversion utilities, validation (using Zod),helper functions in lib/utils