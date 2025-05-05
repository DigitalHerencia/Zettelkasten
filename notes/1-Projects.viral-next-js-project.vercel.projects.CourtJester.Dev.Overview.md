---
id: 77o7qq0pie6p8o7spix7znf
title: Overview
desc: ''
updated: 1742100829435
created: 1742099415713
---

# Project Overview

Court Jester is a web application designed to help inmates track their legal cases, receive notifications about hearings and case updates, and generate legal motions. It provides an admin interface for managing offenders, cases, and notifications, and an offender interface for inmates to access their information.

The application is built with Next.js 15, using the App Router architecture, and is designed to be deployed on Vercel. It currently uses Vercel Blob for storage but needs to be transitioned to MongoDB for production.

## Directory Structure

```plaintext
court-jester/
├── app/
│   ├── admin/
│   │   ├── cases/
│   │   │   └── [id]/
│   │   │       └── page.tsx
│   │   ├── dashboard/
│   │   │   └── page.tsx
│   │   ├── motions/
│   │   │   └── [id]/
│   │   │       └── page.tsx
│   │   └── offenders/
│   │       ├── [id]/
│   │       │   ├── cases/
│   │       │   │   └── route.ts
│   │       │   └── page.tsx
│   │       └── route.ts
│   ├── api/
│   │   ├── admin/
│   │   │   ├── cases/
│   │   │   │   └── [id]/
│   │   │   │       └── route.ts
│   │   │   ├── documents/
│   │   │   │   └── upload/
│   │   │   │       └── route.ts
│   │   │   ├── motions/
│   │   │   │   ├── [id]/
│   │   │   │   │   ├── pdf/
│   │   │   │   │   │   └── route.ts
│   │   │   │   │   └── route.ts
│   │   │   │   └── route.ts
│   │   │   ├── notifications/
│   │   │   │   ├── [id]/
│   │   │   │   │   └── route.ts
│   │   │   │   └── route.ts
│   │   │   ├── offenders/
│   │   │   │   ├── [id]/
│   │   │   │   │   └── route.ts
│   │   │   │   ├── mugshot/
│   │   │   │   │   └── route.ts
│   │   │   │   └── profile/
│   │   │   │       └── route.ts
│   │   │   ├── reminders/
│   │   │   │   ├── [id]/
│   │   │   │   │   └── route.ts
│   │   │   │   ├── cron-status/
│   │   │   │   │   └── route.ts
│   │   │   │   ├── process/
│   │   │   │   │   └── route.ts
│   │   │   │   └── route.ts
│   │   │   └── search/
│   │   │       ├── cases/
│   │   │       │   └── route.ts
│   │   │       ├── inmate/
│   │   │       │   └── route.ts
│   │   │       └── route.ts
│   │   ├── auth/
│   │   │   └── login/
│   │   │       └── route.ts
│   │   ├── help-content/
│   │   │   └── route.ts
│   │   ├── offender/
│   │   │   ├── cases/
│   │   │   │   ├── [id]/
│   │   │   │   │   └── route.ts
│   │   │   │   └── route.ts
│   │   │   ├── motions/
│   │   │   │   ├── [id]/
│   │   │   │   │   ├── pdf/
│   │   │   │   │   │   └── route.ts
│   │   │   │   │   └── route.ts
│   │   │   │   └── route.ts
│   │   │   ├── notifications/
│   │   │   │   ├── [id]/
│   │   │   │   │   └── route.ts
│   │   │   │   └── route.ts
│   │   │   ├── profile/
│   │   │   │   └── route.ts
│   │   │   └── reminders/
│   │   │       ├── [id]/
│   │   │       │   └── route.ts
│   │   │       └── route.ts
│   │   ├── test/
│   │   │   └── route.ts
│   │   └── test-simple/
│   │       └── route.ts
│   ├── confirmation/
│   │   └── page.tsx
│   ├── globals.css
│   ├── layout.tsx
│   ├── loading/
│   │   └── page.tsx
│   ├── offender/
│   │   ├── cases/
│   │   │   └── [id]/
│   │   │       └── page.tsx
│   │   ├── login/
│   │   │   └── page.tsx
│   │   ├── notifications/
│   │   │   └── page.tsx
│   │   ├── profile/
│   │   │   └── page.tsx
│   │   └── reminders/
│   │       └── page.tsx
│   └── page.tsx
├── components/
│   ├── confirmation-dialog.tsx
│   ├── document-processing-tab.tsx
│   ├── floating-help-button.tsx
│   ├── help-button.tsx
│   ├── help-menu-item.tsx
│   ├── help-modal.tsx
│   ├── keyboard-help-shortcut.tsx
│   ├── markdown-renderer.tsx
│   ├── motion-editor.tsx
│   ├── motion-history.tsx
│   ├── reminder-form.tsx
│   ├── reminder-list.tsx
│   └── ui/
│       ├── badge.tsx
│       ├── dialog.tsx
│       ├── progress.tsx
│       ├── switch.tsx
│       └── ... (other UI components)
├── lib/
│   ├── actions.ts
│   ├── auth.ts
│   ├── db/
│   │   ├── blob-storage.ts
│   │   └── models.ts
│   ├── motion-templates.ts
│   ├── notifications.ts
│   ├── utils.ts
│   └── utils/
│       ├── case-parser.ts
│       ├── error-handler.ts
│       ├── inmate-search.ts
│       ├── profile-parser.ts
│       └── validation.ts
├── middleware.ts
├── monaco-environment.ts
├── package.json
├── public/
│   ├── fonts/
│   │   ├── jacquard-24-charted.woff2
│   │   └── kings.woff2
│   └── sw.js
├── tailwind.config.ts
└── vercel.json
```

## Mock/Simulated Code and Data

The project currently uses extensive mock data and simulated API endpoints. Here's a breakdown:

### Mock Data Sources

1. **In-memory Storage**:

- `app/api/auth/login/route.ts` uses `MEMORY_STORAGE` object for sessions, offenders, and notifications

2. **Hard-coded Mock Data**:

- `app/api/admin/notifications/route.ts` - Mock notifications
- `app/api/admin/search/route.ts` - Mock offenders
- `app/api/admin/offenders/[id]/route.ts` - Mock offender data
- `app/api/admin/offenders/[id]/cases/route.ts` - Mock cases
- `lib/utils/inmate-search.ts` - `TEST_OFFENDER` object with mock data
- `lib/actions.ts` - Fallback mock data for offenders and cases
  
3. **Simulated API Responses**:

- `app/api/admin/motions/[id]/pdf/route.ts` - Returns a mock PDF
- `app/api/offender/motions/[id]/pdf/route.ts` - Redirects to a mock PDF endpoint

### Simulated Functionality

1. **Authentication**:

- Uses in-memory storage instead of a proper auth system
- Special "GRINGO" code for language switching

2. **Search Functionality**:

- `app/api/admin/search/inmate/route.ts` - Returns mock data for inmate 468079
- `app/api/admin/search/cases/route.ts` - Returns mock data for "CHRISTOPHER DOMINGUEZ"

3. **Document Processing**:

- `lib/utils/profile-parser.ts` and `lib/utils/case-parser.ts` - Simulated parsing logic

## API Endpoints and Data Retrieval

### Authentication Endpoints

1. **POST /api/auth/login**

- **Purpose**: Authenticate users (inmates or admins)
- **Data**: `{ inmateNumber: string }`
- **Logic**: Validates inmate number, creates session, sets cookie
- **Storage**: Session data in blob storage

## Package Dependencies

### Production Dependencies

```json
{
  "dependencies": {
    "@radix-ui/react-accordion": "^1.2.3",
    "@radix-ui/react-alert-dialog": "^1.1.6",
    "@radix-ui/react-aspect-ratio": "^1.1.2",
    "@radix-ui/react-avatar": "^1.1.3",
    "@radix-ui/react-checkbox": "^1.1.4",
    "@radix-ui/react-context-menu": "^2.2.6",
    "@radix-ui/react-context": "^1.1.1",
    "@radix-ui/react-dialog": "^1.1.6",
    "@radix-ui/react-dropdown-menu": "^2.1.6",
    "@radix-ui/react-hover-card": "^1.1.6",
    "@radix-ui/react-icons": "^1.3.2",
    "@radix-ui/react-label": "^2.1.2",
    "@radix-ui/react-menubar": "^1.1.6",
    "@radix-ui/react-navigation-menu": "^1.2.5",
    "@radix-ui/react-popover": "^1.1.6",
    "@radix-ui/react-progress": "^1.1.2",
    "@radix-ui/react-radio-group": "^1.2.3",
    "@radix-ui/react-scroll-area": "^1.2.3",
    "@radix-ui/react-select": "^2.1.6",
    "@radix-ui/react-separator": "^1.1.2",
    "@radix-ui/react-slider": "^1.2.3",
    "@radix-ui/react-slot": "^1.1.2",
    "@radix-ui/react-switch": "^1.1.3",
    "@radix-ui/react-tabs": "^1.1.3",
    "@radix-ui/react-toast": "^1.2.6",
    "@radix-ui/react-toggle-group": "^1.1.2",
    "@radix-ui/react-toggle": "^1.1.2",
    "@radix-ui/react-tooltip": "^1.1.8",
    "@vercel/blob": "^0.22.1",
    "class-variance-authority": "^0.7.1",
    "clsx": "^2.1.1",
    "cmdk": "^1.0.4",
    "date-fns": "^4.1.0",
    "framer-motion": "^10.16.4",
    "lucide-react": "^0.479.0",
    "nanoid": "^5.0.6",
    "next": "15.2.2",
    "next-themes": "^0.4.6",
    "puppeteer": "^24.4.0",
    "react": "19.0.0",
    "react-dom": "19.0.0",
    "react-markdown": "^9.0.1",
    "tailwind-merge": "^3.0.2",
    "tailwindcss": "^4.0.14",
    "tailwindcss-animate": "^1.0.7",
    "typescript": "^5.8.2",
    "zod": "^3.22.4"
  }
}
```

### Development Dependencies

```json
{
  "devDependencies": {
    "@tailwindcss/typography": "^0.5.10",
    "@types/node": "^22.13.10",
    "@types/react": "^19.0.10",
    "@types/react-dom": "^19.0.4",
    "autoprefixer": "^10.4.21",
    "eslint": "^9.22.0",
    "eslint-config-next": "^15.2.2",
    "postcss": "^8.5.3"
  }
}
```

## Known Issues and Broken Functionality

### 1. **Build Error**:

1. Error in `lib/motion-templates.ts` with template variables causing build failure
2. Fixed by properly formatting template variables without spaces inside curly braces

### 2. **Vercel Blob in Edge Runtime**:

1. Warning about Node.js modules in Edge Runtime
2. Solution: Ensure Vercel Blob is only used in Server Components or API routes

### 3. **Authentication**:

1. Using in-memory storage for sessions
2. No proper authentication mechanism
3. No password protection

### 4. **Mock Data**:

1. Extensive use of mock data throughout the application
2. No real database integration

### 5. **PDF Generation**:

1. Mock PDF generation in motion endpoints
2. No real PDF generation functionality

### 6. **External API Integration**:

1. Simulated inmate search and case search
2. No real integration with external systems

### 7. **Error Handling**:

1. Inconsistent error handling across API routes
2. Some routes use proper error handling, others don't

### 8. **Validation**:

1. Incomplete input validation
2. No comprehensive validation strategy

### 9. **Security**:

1. No CSRF protection
2. No rate limiting
3. No proper authentication

### 10. **Accessibility**:

1. Some accessibility issues in UI components
2. Missing aria attributes in some places
