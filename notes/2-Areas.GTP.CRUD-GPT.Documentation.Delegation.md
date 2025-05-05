---
id: dgbgfogl8gnkpdihubxgdbw
title: Delegation
desc: ''
updated: 1742530209534
created: 1742530205371
---
### **Key Roles & Responsibilities**

Think of this system like a **team of AI assistants**, each handling different parts of the stack:

#### **1. App Team (Frontend Pages & API Routes)**

- **Frontend Prompter GPT** → Breaks down feature requests into frontend tasks.
- **Frontend Worker GPT** → Generates Next.js pages & UI components.
- **Frontend QA GPT** → Reviews frontend code for best practices.
- **API Prompter GPT** → Defines API endpoints, request structures.
- **API Worker GPT** → Builds API routes in Next.js.
- **API QA GPT** → Validates API implementation & error handling.

#### **2. Components Team (UI/UX)**

- **Component Prompter GPT** → Defines reusable UI components.
- **Component Worker GPT** → Generates ShadCN/Tailwind components.
- **Component QA GPT** → Ensures consistency & accessibility.

#### **3. Lib Team (Backend Logic & Data)**

- **Model Prompter GPT** → Defines Mongoose schema structures.
- **Model Worker GPT** → Generates MongoDB schemas.
- **Model QA GPT** → Validates database models.
- **Utils Prompter GPT** → Defines utility functions & helpers.
- **Utils Worker GPT** → Generates backend utilities.
- **Utils QA GPT** → Ensures security & performance.
- **Auth Prompter GPT** → Handles authentication/Clerk integration.
- **Auth Worker GPT** → Generates middleware & ABAC rules.
- **Auth QA GPT** → Validates security implementations.

#### **4. CI/CD & Deployment Team**

- **CI Prompter GPT** → Defines testing & CI pipelines.
- **CI Worker GPT** → Generates GitHub Actions workflows.
- **CI QA GPT** → Validates pipeline setup.
- **Deploy Prompter GPT** → Generates deployment configurations.
- **Deploy Worker GPT** → Builds Vercel configs.
- **Deploy QA GPT** → Checks for deployment issues.

#### **5. Type System Team (Cross-Cutting)**

- **Type Checker Prompter GPT** → Defines TypeScript structures.
- **Type Checker Worker GPT** → Ensures type safety.
- **Type Checker QA GPT** → Fixes TypeScript-related errors.

* * *