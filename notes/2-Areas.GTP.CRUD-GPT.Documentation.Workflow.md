---
id: orw1kgzbp8uss2iqnmu9x5d
title: Workflow
desc: ''
updated: 1742530168769
created: 1742530165196
---
### **Project Workflow**

Here’s the **lifecycle of how we build features**:

1. **Pre-Production (Planning & Breakdown)**

    - Take a user story or idea (e.g., "Create a login page").
    - The **Frontend Page Prompter GPT**breaks it down into:
        - Page requirements (inputs, buttons, API calls).
        - UI design references (ShadCN components, Tailwind styles).
        - Expected file structure (where the code will go).
    - The **API Prompter GPT**defines backend needs:
        - API endpoints, request structure, response shape.
        - Database interactions (Mongoose models, queries).
        - Authentication and permissions.
2. **Prototyping (Code Generation)**

    - Each workgroup **Worker GPT**generates the actual code:
        - **Frontend Worker GPT** → Creates Next.js pages & components.
        - **API Worker GPT** → Builds API routes in Next.js.
        - **Model Worker GPT** → Defines Mongoose schemas & validation.
    - The user **copies the generated code** into the project directory.
3. **Validation & Debugging**

    - Each **QA Checker GPT**runs validation:
        - **Frontend QA GPT** ensures UI is correct, accessible, and responsive.
        - **Backend QA GPT** checks security, API correctness, and error handling.
        - **Type System QA GPT** ensures TypeScript correctness and proper typing.
    - If errors are found, the **QA GPT suggests fixes**, which can be fed back to the **Worker GPT** for refinement.
4. **Development & Deployment**

    - Once the code is solid:
        - The project is **tested locally** (`npm run dev`).
        - Code is committed to **GitHub**.
        - A GitHub Action (created by the **CI/CD Worker GPT**) runs tests & lints the code.
        - **Vercel Deployment GPT** generates deployment configurations.
        - The project is **deployed to Vercel** with automatic preview deployments.
5. **Maintenance & Iterations**

    - Updates, bug fixes, and optimizations go through the **same cycle**.
    - The AI system can also generate **documentation** for the repo.

* * *