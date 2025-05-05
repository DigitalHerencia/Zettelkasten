---
id: igs7x4kjwsy8kqrz3vu0pb1
title: Dev
desc: ''
updated: 1742226599574
created: 1742225559820
---
# Court Jester  🤡  (Next.js, TypeScript, MongoDB, ShadCN UI, Tailwind CSS)
## A Viral Next.js Project for the New Mexico Courts
___

# Table of Contents

1.  **Codebase Assessment & Local Development Checklist**  
    1.1. Overview of the Codebase Architecture  
    1.2. Detailed Component Analysis (Pages, API Endpoints, Client Components)  
    1.3. Checklist for Running on Local Host and Verifying Functionality

![[DetailedCodebaseAssessment|1-Projects.viral-next-js-project.vercel.projects.CourtJester.Rebuild.DetailedCodebaseAssessment]]

2.  **Authentication & Authorization System**  
    2.1. Offender (User) Authentication Using Inmate Number  
    2.2. Admin Authentication Using a Fixed Code (“admin86”)  
    2.3. Session Management: HTTP‑Only Cookies and JWT Tokens  
    2.4. API Endpoints for Login/Registration  
    2.5. Zod Validation for Input Verification

![[Aut|1-Projects.viral-next-js-project.vercel.projects.CourtJester.Rebuild.Dev.Auth]]

3.  **Interactive API Concepts Lesson**  
    3.1. Basic API Vocabulary and Concepts  
    3.2. Next.js App Router API Routes  
    3.3. HTTP Methods (GET, POST, PATCH, DELETE) with Examples  
    3.4. Error Handling in API Endpoints and Security Considerations  
    3.5. TypeScript Integration and Type Safety in API Calls

![[Legacy|1-Projects.viral-next-js-project.vercel.projects.CourtJester.Rebuild.Dev.API.Legacy]]

3.  **Interactive API Concepts Lesson**  
    3.1. Basic API Vocabulary and Concepts  
    3.2. Next.js App Router API Routes  
    3.3. HTTP Methods (GET, POST, PATCH, DELETE) with Examples  
    3.4. Error Handling in API Endpoints and Security Considerations  
    3.5. TypeScript Integration and Type Safety in API Calls

![[Lesso|1-Projects.viral-next-js-project.vercel.projects.CourtJester.Rebuild.Dev.API.Lesson]]

4.  **Offender Services & Document Parsing**  
    4.1. Overview of Offender Services (Reminders, Notifications, Alarms)  
    4.2. Workflow: New Offender Registration and Profile Setup  
    4.3. PDF Upload and Parsing (Using Packages Like pdf‑parse)  
    4.4. Parsing Form Text from DOC Data  
    4.5. Notifying Offenders When Their Profile Is Ready  
    4.6. API Endpoints for Document Processing

![[Auth|1-Projects.viral-next-js-project.vercel.projects.CourtJester.Rebuild.Plan.Sections.Auth]]

5.  **Motion Management System**  
    5.1. Motion Templates: Library of Standard Motions  
    5.2. Auto‑Population of Motion Templates Using Offender Data  
    5.3. Fill‑in‑the‑Blank Editor for Admins (Rich Text Editors such as React Quill)  
    5.4. API Endpoints for Creating, Updating, and Deleting Motions  
    5.5. Offender Interaction: Viewing, Downloading (PDF Generation), and Deleting Motions  
    5.6. Notification Workflow for New Motions

![[Notifications|1-Projects.viral-next-js-project.vercel.projects.CourtJester.Rebuild.Plan.Sections.Notifications]]

6.  **MongoDB Integration & Schema Management**  
    6.1. Overview of MongoDB Collections (Offenders, Notifications, Motions, Templates)  
    6.2. Defining Schemas with Mongoose (or Native Driver)  
    \- Offender Schema Example  
    \- Notification Schema Example  
    \- Motion Schema Example  
    \- Template Schema Example  
    6.3. CRUD Operations and Database Functions  
    6.4. Differentiating Persistent Data (MongoDB) from Session Data (Cookies/JWT)

![[Registration|1-Projects.viral-next-js-project.vercel.projects.CourtJester.Rebuild.Plan.Sections.Registration]]

7.  **ShadCN UI Components & Design System**  
    7.1. Organizing UI Components (Folder Structure and Naming Conventions)  
    7.2. Core Components: Card, Button, Input, Tabs, Badge, ConfirmationDialog, Toaster  
    7.3. Responsive, Mobile‑First Design Principles  
    7.4. Integrating Tailwind CSS: Colors, Fonts (Jacquard for Headings, Kings for Body), and Spacing  
    7.5. Layout Examples: Admin Dashboard & Offender Profile with Tabbed Interfaces  
    7.6. Best Practices for Using ShadCN UI with Tailwind

![[ShadCN|1-Projects.viral-next-js-project.vercel.projects.CourtJester.Rebuild.Plan.Sections.ShadCN]]

8.  **TypeScript Interfaces & API Types**  
    8.1. Centralizing Types and Interfaces (Creating a /types Folder)  
    8.2. Defining Domain Models (Offender, Notification, Motion, Template)  
    8.3. API Payload Interfaces (Requests and Responses)  
    8.4. Component Prop Types and React Hook Form Integration  
    8.5. Using Zod for Runtime Validation and Type Inference  
    8.6. Best Practices for Strict TypeScript Settings and tsconfig.json Configuration

![[Types|1-Projects.viral-next-js-project.vercel.projects.CourtJester.Rebuild.Plan.Sections.Types]]

9.  **Error Handling & Loading States**  
    9.1. API Error Handling: Try/Catch, Logging, and HTTP Status Codes  
    9.2. Client-Side Error Handling and Redirects (useRouter for Redirects)  
    9.3. Next.js Error Boundaries: Creating error.tsx for Route Segments  
    9.4. Loading States: Creating loading.tsx for Fallback UI During Data Fetching  
    9.5. Integrating Toasts for Immediate, Transient Feedback  
    9.6. Holistic Error Management Workflow and Best Practices

![[ErrorHandling|1-Projects.viral-next-js-project.vercel.projects.CourtJester.Rebuild.Plan.Sections.ErrorHandling]]

10.  **Design System (ShadCN) Best Practices**  
    10.1. Following the ShadCN Design System Guidelines  
    10.2. Organizing Design Tokens and Tokens in a /design-tokens Folder  
    10.3. Using Tailwind CSS Utility Classes and Color Functions  
    10.4. Creating a Design System Reference Page with Storybook  
    10.5. Integrating Design System Components with Next.js Pages and API Routes  
    10.6. Best Practices for Maintaining a Living Design System

![[DesignSystem|1-Projects.viral-next-js-project.vercel.projects.CourtJester.Rebuild.Plan.Sections.DesignSystem]]

11.  **Offender Services: Profile, Cases, Motions, Reminders, Notifications**  
    11.1. Overview of Offender Services and How They Fit into the App  
    11.2. Creating the Offender Profile Page with Tabs for Cases, Motions, Reminders, and Notifications  
    11.3. Implementing the Offender Profile Page with Dynamic Route Parameters  
    11.4. Integrating Offender Services with API Endpoints and MongoDB  

![[OffenderServices|1-Projects.viral-next-js-project.vercel.projects.CourtJester.Rebuild.Plan.Sections.OffenderServices]]

12.  **Motions: CRUDE Operations and Database Functions**  
    12.1. Overview of Motions and How They Fit into the App  
    12.2. Creating the Motions Page with CRUD Operations and Dynamic Route Parameters  
    12.3. Implementing the Motions Page with API Endpoints and MongoDB  

![[Motions|1-Projects.viral-next-js-project.vercel.projects.CourtJester.Rebuild.Plan.Sections.Motions]]

13.  **MongoDB Integration & Schema Management**  
    13.1. Overview of MongoDB Collections (Offenders, Notifications, Motions, Templates)  
    13.2. Defining Schemas with Mongoose (or Native Driver)  
    \- Offender Schema Example  
    \- Notification Schema Example  
    \- Motion Schema Example  
    \- Template Schema Example  
    13.3. CRUD Operations and Database Functions  
    13.4. Differentiating Persistent Data (MongoDB) from Session Data (Cookies/JWT)

![[Mongodb|1-Projects.viral-next-js-project.vercel.projects.CourtJester.Rebuild.Plan.Sections.Mongodb]]



