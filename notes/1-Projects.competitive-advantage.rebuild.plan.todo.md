---
id: 4r8pebp5fegl5yqfucquh35
title: todo
desc: ''
updated: 1727238654055
created: 1727235909386
---

# TODO

## Important:

1.  **Frontend Migration**:
    
    -   [ ]  Set up Next.js project.
    -   [ ]  Migrate existing React components into Next.js pages.
    -   [ ]  Implement SSR and SSG.
2.  **Backend Refactor**:
    
    -   [ ]  Set up NestJS for backend.
    -   [ ]  Refactor Express routes into NestJS controllers.
3.  **State Management**:
    
    -   [ ]  Implement Recoil for state management.
    -   [ ]  Refactor existing Redux actions to Recoil atoms.
4.  **Database**:
    
    -   [ ]  Create MongoDB aggregation queries for sales data.
    -   [ ]  Ensure proper indexing in MongoDB.
5.  **CI/CD**:
    
    -   [ ]  Set up GitHub Actions workflow for automated deployments.
    -   [ ]  Configure Vercel for automatic frontend deployments.

## Todo List for Developers:

### Frontend (React + Next.js Migration)
    
-   [ ]  Replace `react-router-dom` with Next.js native routing.
-   [ ]  Refactor state management from Redux to Recoil.
-   [ ]  Implement SSR for dynamic product and market share pages.
-   [ ]  Optimize Nivo charts by memoizing expensive operations.
-   [ ]  Migrate and restructure React components to Next.js pages.

### Backend (Node.js + NestJS Migration)

-   [ ]  Migrate from Express to NestJS, implementing service modules for products, reports, and user management.
-   [ ]  Refactor database calls to use MongoDB's aggregation pipelines and ensure indexing for high-frequency fields.
-   [ ]  Add Redis caching for common API requests.
-   [ ]  Implement JWT-based authentication in NestJS with role-based guards.

### Database Layer (MongoDB)

-   [ ]  Implement proper indexing for collections such as `product_id`, `zip_code`, and `sales_data`.
-   [ ]  Optimize MongoDB queries using aggregation pipelines.
-   [ ]  Enable automatic scaling and backups on MongoDB Atlas.

### State Management (Redux to Recoil)

-   [ ]  Remove Redux and implement Recoil atoms and selectors.
-   [ ]  Optimize components with `useMemo` and `useCallback` to prevent unnecessary re-renders.
-   [ ]  Implement context-based state management where global state is not necessary.

### Deployment Strategy

-   [ ]  Deploy frontend on Vercel using Next.js (serverless deployment).
-   [ ]  Deploy backend API on AWS Lambda using Serverless Framework.
-   [ ]  Set up CI/CD with GitHub Actions for automatic deployments and testing.
-   [ ]  Implement Docker for containerization and use it in local development.

### Improved DevOps 

-   [ ]  Set up GitHub Projects for task management.
-   [ ]  Install and configure Prettier, ESLint, and other relevant VS Code extensions.
-   [ ]  Configure GitHub branch protection and review workflows.
    
