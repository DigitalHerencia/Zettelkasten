---
id: ttyequanwpjf2hxqx69qejr
title: readme
desc: ''
updated: 1744670643810
created: 1741487414119
---
###  Court Jester

**Tu camarada en la sombra** - Your companion in the shadows

Court Jester is a web application designed to help users track inmate information, court dates, and legal motions. It provides a streamlined interface for searching inmate records across different correctional systems, tracking court dates, and generating legal motions.

## Table of Contents

- [Project Overview](#project-overview)
- [Installation & Setup](#installation--setup)
- [Admin Access](#admin-access)
- [Testing Guide](#testing-guide)
- [Settings & Preferences](#settings--preferences)
- [UI/UX Design](#uiux-design)
- [Project Structure](#project-structure)
- [Troubleshooting](#troubleshooting)


## Project Overview

Court Jester is built with Next.js and uses a combination of server-side and client-side technologies to provide a seamless experience for users tracking legal information. The application includes:

- Inmate search across multiple correctional systems (NMDC, BOP)
- Court date tracking and notifications
- Legal motion generation and management
- User settings and preferences
- Mobile-friendly interface


## Installation & Setup

### Prerequisites

- Node.js 18.x or higher
- npm or yarn
- Vercel account (for deployment)


### Local Development

1. Clone the repository:

```shellscript
git clone https://github.com/your-username/court-jester.git
cd court-jester
```


2. Install dependencies:

```shellscript
npm install
```


3. Create a `.env.local` file with the following variables:

```plaintext
CAPTCHA_SERVICE_API_KEY=your_captcha_service_key
BLOB_READ_WRITE_TOKEN=your_vercel_blob_token
```


4. Start the development server:

```shellscript
npm run dev
```


5. Open [http://localhost:3000](http://localhost:3000) in your browser.


### Deployment

The application is designed to be deployed on Vercel:

1. Push your code to a GitHub repository
2. Connect the repository to Vercel
3. Configure the environment variables in the Vercel dashboard
4. Deploy


## Admin Access

Court Jester includes an admin mode for testing and maintenance purposes.

### Accessing Admin Mode

1. On the login page, enter an admin code in the format `ADMIN-123456`
2. The system will load mock data for testing purposes


### Admin Features

- View mock inmate data
- Test notification system
- Generate sample motions
- Access all features without real data dependencies


### Admin Codes

- `ADMIN-000000` - Basic admin access with minimal mock data
- `ADMIN-111111` - Admin access with comprehensive mock data including court dates
- `ADMIN-222222` - Admin access with error simulation for testing


## Testing Guide

### Manual Testing

#### Inmate Search Testing

1. **NMDC Search**:

1. Use a 6-digit number format (e.g., `488079`)
2. Verify that the search progress indicators work correctly
3. Confirm that inmate details are displayed correctly



2. **BOP Search**:

1. Use the format `#####-###` (e.g., `12345-678`)
2. Verify that the search progress indicators work correctly
3. Confirm that inmate details are displayed correctly



3. **Admin Mode**:

1. Use the format `ADMIN-######` (e.g., `ADMIN-111111`)
2. Verify that mock data is loaded correctly





#### Court Date Search Testing

1. Navigate to the dashboard after a successful inmate search
2. Verify that court dates are displayed correctly
3. Test the notification settings for court dates


#### Motion Generation Testing

1. Navigate to the motions page
2. Test creating different types of motions
3. Verify that the generated motions contain the correct information


### Automated Testing

Currently, the project does not include automated tests. This is a planned feature for future development.

## Settings & Preferences

Court Jester includes several user settings and preferences that can be configured:

### Language Settings

- **Spanglish (Default)**: A mix of Spanish and English commonly used in border regions
- **English**: Full English interface
- **Spanish**: Full Spanish interface


### Notification Settings

- **Enable Notifications**: Toggle all notifications on/off
- **Court Date Reminders**: Receive reminders for upcoming court dates
- **Reminder Timing**: Configure when to receive reminders (day before, morning of, hour before)


### Privacy Settings

- **Store Data Locally**: Toggle whether to store data in the browser's local storage
- **Anonymous Mode**: Use the app without storing any identifiable information
- **Secure Mode**: Automatically clear data when the app is closed


### Motion Preferences

- **Enable Motions**: Toggle the motion generation feature on/off
- **Default Court**: Set the default court for generated motions


## UI/UX Design

Court Jester's design is inspired by playing cards and jester imagery, with a focus on accessibility and ease of use.

### Design Principles

1. **Simplicity**: Minimalist interface with clear navigation
2. **Accessibility**: High contrast colors and readable text
3. **Mobile-First**: Designed for mobile devices with a responsive layout
4. **Visual Hierarchy**: Important information is visually emphasized


### Color Scheme

- **Primary Color**: `#ff5500` (Orange-Red) - Used for buttons and important elements
- **Background Color**: `#f5e6c9` (Light Beige) - Reminiscent of parchment or playing cards
- **Text Color**: `#333333` (Dark Gray) - Provides good contrast against the background
- **Accent Colors**: Various shades of gray and red for highlighting and contrast


### Key UI Components

1. **Login Page**: Simple form with the Court Jester logo and a search input
2. **Search Progress**: Visual indicators showing the progress of the search operation
3. **Dashboard**: Overview of inmate information and upcoming court dates
4. **Bottom Navigation**: Mobile-friendly navigation for accessing key features
5. **Motion Generator**: Form-based interface for creating legal motions


### User Flow

1. User enters an inmate number on the login page
2. System searches for the inmate across multiple databases
3. If found, user is taken to the dashboard showing inmate information
4. User can navigate to court dates, motions, or settings
5. User can log out, which clears session data based on privacy settings


## Project Structure

```plaintext
court-jester/
├── app/ ✅ - Application routes and pages
│   ├── api/ ✅ - API routes for data fetching and processing
│   │   ├── date-search/ ✅ - Court date search functionality
│   │   ├── inmate-search/ ✅ - Inmate search across systems
│   │   └── user-services/ ✅ - User-specific services (motions, notifications, settings)
│   ├── cases/ ✅ - Case management pages
│   ├── court-dates/ ✅ - Court date tracking pages
│   ├── dashboard/ ✅ - Main dashboard after login
│   ├── motions/ ✅ - Motion generation and management
│   ├── notifications/ ✅ - Notification management
│   ├── privacy/ ✅ - Privacy settings page
│   ├── root/ ✅ - Login page and authentication
│   ├── search/ ✅ - Advanced search functionality
│   ├── settings/ ✅ - User settings management
│   ├── globals.css ✅ - Global styles
│   ├── layout.tsx ✅ - Root layout component
│   └── page.tsx ✅ - Root page (redirects to /root)
├── components/ ✅ - Reusable UI components
│   ├── bottom-nav.tsx ✅ - Mobile navigation bar
│   ├── dashboard/ ✅ - Dashboard-specific components
│   ├── logo.tsx ✅ - Logo component
│   ├── mode-toggle.tsx ✅ - Theme toggle component
│   ├── root/ ✅ - Login page components
│   │   ├── progress-step.tsx ✅ - Progress indicator component
│   │   └── search-progress.tsx ✅ - Search progress tracking component
│   ├── site-header.tsx ✅ - Header component
│   └── ui/ ✅ - Shadcn UI components
├── lib/ ✅ - Utility functions and services
│   ├── db/ ✅ - Database and storage utilities
│   │   └── blob-storage.ts ✅ - Vercel Blob storage implementation
│   ├── services/ ✅ - Service implementations
│   │   ├── admin-service.ts ✅ - Admin mode functionality
│   │   ├── bop-service.ts ✅ - BOP inmate search
│   │   ├── captcha-service.ts ✅ - CAPTCHA handling
│   │   ├── court-date-service.ts ✅ - Court date search
│   │   ├── motion-service.ts ✅ - Motion generation
│   │   ├── nm-courts-service.ts ✅ - NM Courts search
│   │   ├── nmdc-service.ts ✅ - NMDC inmate search
│   │   ├── notification-service.ts ✅ - Notification management
│   │   └── settings-service.ts ✅ - User settings management
│   ├── types/ ✅ - TypeScript type definitions
│   │   ├── inmate.ts ✅ - Inmate and related data types
│   │   └── search-fields.ts ✅ - Search field definitions
│   ├── utils.ts ✅ - General utility functions
│   └── validation/ ✅ - Input validation
│       └── inmate.ts ✅ - Inmate number validation
├── public/ ✅ - Static assets
│   ├── favicon.ico ✅ - Site favicon
│   └── jester.png ✅ - Jester logo image
├── .env.local.example ✅ - Example environment variables
├── .gitignore ✅ - Git ignore file
├── middleware.ts ✅ - Next.js middleware for request handling
├── next.config.js ✅ - Next.js configuration
├── package.json ✅ - Project dependencies
├── postcss.config.js ✅ - PostCSS configuration
├── README.md 📝 - Project documentation (this file)
├── tailwind.config.js ✅ - Tailwind CSS configuration
└── tsconfig.json ✅ - TypeScript configuration
```

## Troubleshooting

### Common Issues

#### Search Not Working

1. **Issue**: Inmate search fails with no results
**Solution**: Verify that you're using the correct format for the inmate number (6 digits for NMDC, #####-### for BOP)
2. **Issue**: Court date search fails
**Solution**: This could be due to CAPTCHA challenges. Try using admin mode for testing.


#### CAPTCHA Challenges

1. **Issue**: Searches fail due to CAPTCHA challenges
**Solution**: In production, ensure the CAPTCHA_SERVICE_API_KEY is properly configured. For development, the system will wait for manual CAPTCHA solving.


#### Data Persistence

1. **Issue**: Data is lost between sessions
**Solution**: Check the "Store Data Locally" setting in Privacy Settings. If using Secure Mode, data is intentionally cleared when closing the app.


### Support

For additional support, please open an issue on the GitHub repository or contact the development team.