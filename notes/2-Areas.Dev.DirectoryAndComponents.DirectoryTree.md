---
id: cw6chev8twtjm7naw5z3c4k
title: DirectoryTree
desc: ''
updated: 1733466475756
created: 1733465282958
---

### **Directory Tree Structure**

```
    
    my-nextjs-project
    ├── components
    │   ├── Dashboard
    │   │   ├── AdminDashboard.tsx
    │   │   ├── CreatorDashboard.tsx
    │   │   ├── FanDashboard.tsx
    │   ├── shared
    │   │   ├── Button.tsx
    │   │   ├── Card.tsx
    │   │   ├── Modal.tsx
    │   │   ├── Table.tsx
    │   │   ├── Navbar.tsx
    │   │   ├── Footer.tsx
    │   ├── analytics
    │   │   ├── EngagementChart.tsx
    │   │   ├── SubscriptionChart.tsx
    │   ├── forms
    │   │   ├── FeedbackForm.tsx
    │   │   ├── SubscriptionForm.tsx
    ├── lib
    │   ├── auth.ts
    │   ├── prisma.ts
    │   ├── cloudinary.ts
    │   ├── theme.tsx
    │   ├── analytics.ts
    ├── middleware.ts
    ├── pages
    │   ├── api
    │   │   ├── auth
    │   │   │   ├── [...auth0].ts
    │   │   ├── admin
    │   │   │   ├── dashboard.ts
    │   │   ├── creators
    │   │   │   ├── [id]
    │   │   │   │   ├── posts.ts
    │   │   │   │   ├── fans
    │   │   │   ├── [id]
    │   │   │   │   ├── subscriptions.ts
    │   │   ├── posts
    │   │   │   ├── [id].ts
    │   │   │   ├── create.ts
    │   │   ├── upload.ts
    │   ├── admin
    │   │   ├── dashboard.tsx
    │   ├── creators
    │   │   ├── [id]
    │   │   │   ├── dashboard.tsx
    │   ├── fans
    │   │   ├── [id]
    │   │   │   ├── dashboard.tsx
    │   ├── 404.tsx
    │   ├── _app.tsx
    │   ├── _document.tsx
    │   ├── index.tsx
    ├── prisma
    │   ├── schema.prisma
    │   ├── seed.ts
    ├── public
    │   ├── images
    │   │   ├── logo.png
    │   │   ├── placeholders
    │   │   │   ├── avatar.png
    │   │   │   ├── post.png
    ├── styles
    │   ├── globals.css
    │   ├── shadcn.css
    ├── tests
    │   ├── api
    │   │   ├── auth.test.ts
    │   │   ├── adminDashboard.test.ts
    │   ├── components
    │   │   ├── Button.test.tsx
    │   │  ├── Card.test.tsx
    ├── .env.local
    ├── .eslintrc.json
    ├── .prettierrc
    ├── tailwind.config.js
    ├── tsconfig.json
    ├── package.json
    └── README.md

```

* * *

### **Folder and File Details**

#### **1. Components**

- **Dashboard Components**: Individual dashboards for Admin, Creators, and Fans.
- **Shared Components**: Reusable UI elements (Button, Card, Modal, etc.) styled using Tailwind CSS and Shadcn.
- **Analytics Components**: Charts and graphs for displaying engagement metrics and subscriptions.

#### **2. Lib**

- **`auth.ts`**: Middleware and utilities for Auth0 integration and role-based access.
- **`prisma.ts`**: Prisma client setup for database operations.
- **`cloudinary.ts`**: Cloudinary integration for media uploads.
- **`theme.tsx`**: Theme context and provider for light/dark mode toggling.
- **`analytics.ts`**: Functions to fetch and process analytics data.

#### **3. Middleware**

- Centralized **middleware** for protecting API routes and enforcing role-based access control.

#### **4. Pages**

- **API Routes**:
    - `auth/`: Handles Auth0 authentication logic.
    - `admin/`: Fetches admin-level analytics.
    - `creators/`: Manages creator data (e.g., posts, engagement).
    - `fans/`: Handles fan subscriptions and interactions.
    - `posts/`: CRUD operations for posts.
    - `upload.ts`: Endpoint for uploading media to Cloudinary.
- **Frontend Pages**:
    - `admin/dashboard.tsx`: Admin dashboard UI.
    - `creators/[id]/dashboard.tsx`: Creator dashboard UI.
    - `fans/[id]/dashboard.tsx`: Fan dashboard UI.
    - `404.tsx`: Custom 404 error page.

#### **5. Prisma**

- **`schema.prisma`**: Database schema for MongoDB.
- **`seed.ts`**: Script to seed the database with initial data.

#### **6. Public**

- Contains static assets like logos and placeholder images.

#### **7. Styles**

- **`globals.css`**: Base Tailwind CSS styles.
- **`shadcn.css`**: Additional styles for Shadcn components.

#### **8. Tests**

- **API Tests**: Validate the functionality of API endpoints.
- **Component Tests**: Ensure UI components render correctly.

#### **9. Configuration Files**

- **`.env.local`**: Environment variables for sensitive data (e.g., Auth0 keys, MongoDB URL).
- **`tailwind.config.js`**: Tailwind configuration with custom themes and plugins.
- **`tsconfig.json`**: TypeScript configuration.
- **`.eslintrc.json` and `.prettierrc`**: Linting and formatting rules.

* * *

### **Key Notes**

1. **Scalability**: The structure supports adding more features (e.g., notifications, advanced analytics) without major rework.
2. **Reusability**: Shared components ensure consistent UI across the platform.
3. **Testing**: Separate directories for API and component tests make debugging easier.
4. **Deployment**: Vercel-ready, with all environment variables configured in `.env.local`.