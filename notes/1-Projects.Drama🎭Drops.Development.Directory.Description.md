---
id: azl7hqu6e0ldnnh2ayzoswn
title: Description
desc: ''
updated: 1736653055922
created: 1736647855205
---
# **Explanation of Key Folders and Files**

___

#### **`public/`**

Holds static files like the Gadsden Panthers logo, fonts, and background images for branding.

#### **`prisma/`**

Manages database schema and migrations for MongoDB with Prisma.

#### **`app/`**

Uses Next.js App Router structure:

-   **`api/`**: Contains API routes (e.g., for posts, reactions, and Auth0).
-   **`dashboard/`**: Contains the main dashboard where students interact with posts and reactions.
-   **`layout.tsx`**: Global layout components (navigation, branding).
-   **`theme.ts`**: Custom Shadcn UI theme for Gadsden Panthers branding.
-   **`styles/`**: Global styles, integrated with TailwindCSS and Shadcn.

#### **`components/`**

Holds reusable UI components (e.g., `Navbar`, `PostCard`, `ReactionBar`).

#### **`hooks/`**

Custom React hooks to simplify state and API interactions.

#### **`lib/`**

Utility functions and configurations for Prisma, API fetching, and Auth0 integration.

#### **`tests/`**

Unit and integration tests for components, pages, and APIs.
