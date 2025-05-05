---
id: q12ef66rga0kddkxit6wmmf
title: stack
desc: ''
updated: 1744746509919
created: 1741287073038
---
# Tech Stack Overview

A modern, scalable, and modular **web application architecture** built with **cutting-edge frameworks and cloud-native deployments**. The stack prioritizes **developer efficiency, performance, and reactivity**, leveraging **Next.js, React 19, and TypeScript** for a streamlined, serverless-first approach.

* * *

## Core Development Stack
#### (All at Latest Versions)

- **Frontend Framework**: `Next.js` (App Router + Advanced Routing)
- **UI & Components**:
    - `React.js` (Component-driven UI, SSR & ISR support)
    - `ShadCN` (Highly customizable, accessible UI)
    - `Tailwind CSS` (Utility-first styling, mobile-first design)
    - `Lucide Icons` (Lightweight, modern SVG icons)
    - `ShadCN Charts` (Integrated, performant visualizations)
- **State Management**: `Redux Toolkit/RTK Query` (Optimized API state management)
- **Data Fetching & APIs**:
    - `Mapbox` (Interactive maps & geospatial data)
    - `RTK Query` (Client-side API caching & querying)
- **Code Quality & Formatting**:
    - `ESLint` (Static analysis for best practices)
    - `Prettier` (Code formatting & consistency)

## Development Environment

- **OS & Terminal**:
    - `Windows 11 Pro`
    - `PowerShell Terminal` (Scripting & automation)
- **Package & Dependency Management**:
    - `NPM/NVM` (Node.js package management)
    - `Winget` (Windows package manager for CLI tools)

* * *

## Production & Deployment

#### Activated in Production Only

- **Hosting & CI/CD**: `Vercel` (Optimized serverless deployment, previews, auto-scaling)
- **Storage & Compute**:
    - `Vercel Blob` (Edge storage for media & assets)
    - `Vercel Fluid Compute` (Dynamic, efficient compute scaling)
- **Authentication & Security**:
    - `Clerk` (Modern authentication with ABAC roles: user, mod, admin, dev)
- **Database & ORM**:
    - `MongoDB` (NoSQL document database with aggregation pipelines)
    - `Mongoose` (Schema-based ORM with nested arrays & ObjectIDs)
- **Performance & Optimization**:
    - `PWA` (Progressive Web App capabilities, offline-ready)

* * *

## App Structure 
## & Features

### App/

#### **Primary Modules**

- **Landing Page & Funnel**:
    - `Landing, Funnel Sections (Price, Features, Testimonials, CTA)`
- **Dashboard & Profile**:
    - `Dashboard ([id]), Quick Actions, Fast Links, Notifications, Profile Status`
    - `Profile & Edit Profile`
- **Authentication**:
    - `Webhooks, [login, logout, signup]`
- **API Routes**:
    - `"businesslogic.dbcollection"/route`
- **Pages**:
    - `Features, Settings (Accessibility, Theme, Permissions, Integrations, Preferences)`
    - `Help (README, FAQ, Contact Page)`

* * *

## **Lib/**

### **Utility Modules**

- `Utils`: Conversion utilities, units, Tailwind dependencies, currency, date, compression, cryptology
- `Types`: Strongly-typed params, props, interfaces, and data schemas/models
- `Actions`: CRUD logic for `/api` routes
- `Validations`: `Zod` schemas for form validation
- `Constants`: Navigation links, URLs, app-wide constants
- `Default`: Example dataset for seeding databases & demos
- `Blob`: Vercel Blob storage connections

* * *

## **Components/**

### **Reusable UI Components**

- **Cards**: Main, alt, mini, full-width, image, profile, feature-specific
- **Forms**: Profile, CRUD user input, calendar/schedule, contact info, feature-specific
- **Shared**: Navigation (top nav, bottom bar, sidebar), avatar, quick settings, footer, custom buttons, data tables, charts, mode toggle, search
- **Feature-Specific**: Unique UI elements for specific app features
- **Tools**: Functional UI elements & helper components
- **Landing**: Funnel section components
- **Dashboard**: Dynamic dashboard widgets

* * *

## **Middleware & Configuration**

- `Auth`: Route protection & role-based access control
- `Middleware`: Custom API & business logic enforcement
- `Config Files`: `.ts` or JSON for environment, feature flags, and global settings
- `Global.css`:
    - **Light/Dark mode variables**
    - **Utility classes** for cards, forms, page sections, shared components, typography
    - **Feature-specific styles**

* * *

## **Design & Architectural Principles**

- **Mobile-First Design**: Responsive UI optimized via Tailwind’s container breakpoints
- **Freemium Model**: Pricing tiers with gated premium features
- **Indie Developer Friendly**:
    - **Open Source**
    - **Solo-maintainable architecture**
- **Functional Demo & Simulated Features**:
    - Default seeded database for immediate testing
    - Simulated authentication via “access key”
- **Access Control**:
    - **ABAC (Attribute-Based Access Control)** with user, mod, admin, dev roles
- **Navigation Strategy**:
    - Sidebar for desktop
    - Bottom navigation for mobile
- **Social Engagement Features**:
    - Like, comment, reply, favorite, share

* * *

## **Vercel-Optimized Deployment Strategy**

- **First-Class Vercel Support**: Prioritizing Vercel-native features:
    - Blob storage
    - Fluid compute
    - V0 runtime optimizations
- **Advanced Routing Techniques**:
    - Concurrent Routes
    - Dynamic & Nested Routes
    - Grouped & Catch-All Routes
- **Enhanced User Experience**:
    - Skeleton UI states
    - Loading/error/not-found pages
- **CI/CD Workflow**:
    - **Preview deployments** for feature branches
    - **Separate production environments**
- **Documentation**:
    - In-development README with a Quick Start Guide