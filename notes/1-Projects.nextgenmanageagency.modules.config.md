---
id: kulfprp962xhk0l6r9ciukx
title: config
desc: ''
updated: 1733647035233
created: 1733646586949
---

# Example Configs
    
## **1. `tsconfig.json`: TypeScript Configuration**

#### Purpose

Defines how TypeScript behaves in your project. It controls type-checking, compiler options, and module resolution.

#### Example

```json
{
  "compilerOptions": {
    "target": "esnext", // Specifies ECMAScript target version
    "module": "esnext", // Module system for the project
    "jsx": "preserve", // Preserve JSX in output for React
    "strict": true, // Enable strict type-checking
    "moduleResolution": "node", // Resolve modules like Node.js
    "baseUrl": ".", // Base directory for resolving paths
    "paths": { // Aliases for directories
      "@/components/*": ["components/*"],
      "@/lib/*": ["lib/*"]
    }
  },
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx"], // Files to include
  "exclude": ["node_modules"] // Files to exclude
}


```
* * *

## **2. `.eslintrc.json`: ESLint Configuration**

#### Purpose

Defines linting rules to enforce coding standards and best practices.

#### Example

```json
{
  "env": {
    "browser": true, // Enables browser global variables
    "es2021": true // Enables ECMAScript 2021 features
  },
  "extends": [
    "eslint:recommended", // Default recommended rules
    "plugin:react/recommended", // React-specific linting
    "plugin:@typescript-eslint/recommended", // TypeScript linting
    "prettier" // Disable ESLint rules that conflict with Prettier
  ],
  "parser": "@typescript-eslint/parser", // Use TypeScript parser
  "plugins": ["react", "@typescript-eslint", "prettier"], // Plugins used
  "rules": {
    "prettier/prettier": "error", // Treat Prettier issues as ESLint errors
    "react/react-in-jsx-scope": "off" // Not needed in Next.js
  }
}

```
* * *

## **3. `.prettierrc`: Prettier Configuration**

#### Purpose

Defines code formatting rules.

#### Example

```json
{
  "semi": true, // Use semicolons
  "singleQuote": true, // Use single quotes instead of double quotes
  "tabWidth": 2, // Indent with 2 spaces
  "trailingComma": "es5", // Add trailing commas where valid in ES5
  "printWidth": 80 // Maximum line length
}

```
* * *

## **4. `package.json`: Project Configuration**

#### Purpose

Defines dependencies, scripts, and metadata for your project.

#### Example

```json
{
  "name": "my-nextjs-app",
  "version": "1.0.0",
  "scripts": {
    "dev": "next dev", // Starts the development server
    "build": "next build", // Builds the app for production
    "start": "next start", // Starts the production server
    "lint": "next lint", // Lints the codebase
    "test": "jest" // Runs tests with Jest
  },
  "dependencies": {
    "next": "latest",
    "react": "latest",
    "react-dom": "latest"
  },
  "devDependencies": {
    "typescript": "^4.5.5",
    "eslint": "^8.5.0",
    "prettier": "^2.5.1"
  }
}

```
* * *

## **5. `next.config.js`: Next.js Configuration**

#### Purpose

Customizes Next.js settings, such as enabling plugins, adding headers, or handling images.

#### Example

```javascript
const nextConfig = {
  reactStrictMode: true, // Enforces strict mode in React
  images: {
    domains: ['example.com'], // Allowed domains for external images
  },
  env: {
    API_URL: process.env.API_URL // Makes environment variables accessible
  },
  webpack: (config) => {
    config.resolve.alias['@'] = path.resolve(__dirname);
    return config;
  },
};

module.exports = nextConfig;

```
* * *

## **6. `.env.local`: Environment Variables**

#### Purpose

Stores sensitive data (e.g., API keys) and configurations that shouldn't be hardcoded or committed.

#### Example

```plaintext
DATABASE_URL=mongodb+srv://username:password@cluster.mongodb.net/mydb
API_URL=https://api.example.com
NEXTAUTH_SECRET=your_random_secret
STRIPE_SECRET_KEY=sk_test_12345

```
* * *

## **7. `jest.config.js`: Jest Configuration**

#### Purpose

Configures the Jest testing framework.

#### Example

```javascript
module.exports = {
  testEnvironment: 'jsdom', // Simulates a browser environment
  setupFilesAfterEnv: ['<rootDir>/jest.setup.js'], // Setup file
  moduleNameMapper: {
    '@/components/(.*)': '<rootDir>/components/$1',
    '@/lib/(.*)': '<rootDir>/lib/$1'
  }
};

```
* * *

## **8. `sentry.client.config.js` and `sentry.server.config.js`: Sentry Configuration**

#### Purpose

Configures error monitoring and performance tracking with Sentry.

#### Example (Client)

```javascript
import * as Sentry from '@sentry/nextjs';

Sentry.init({
  dsn: process.env.SENTRY_DSN,
  tracesSampleRate: 1.0, // Adjust sampling for performance monitoring
});

```

#### Example (Server)

```javascript
import * as Sentry from '@sentry/nextjs';

Sentry.init({
  dsn: process.env.SENTRY_DSN,
  tracesSampleRate: 1.0,
});

```
* * *

## **9. `lighthouserc.js`: Lighthouse CI Configuration**

#### Purpose

Automates performance, accessibility, and SEO testing with Lighthouse.

#### Example

```javascript
module.exports = {
  ci: {
    collect: {
      staticDistDir: './out', // Directory to analyze
      url: ['http://localhost:3000'], // URLs to audit
    },
    assert: {
      assertions: {
        'categories:performance': ['error', { minScore: 0.9 }],
        'categories:accessibility': ['warn', { minScore: 1 }],
      },
    },
  },
};

```
* * *

## **10. `lib/cloudinary.js`: Cloudinary Configuration**

#### Purpose

Handles media management and optimization.

#### Example

```javascript
import { v2 as cloudinary } from 'cloudinary';

cloudinary.config({
  cloud_name: process.env.CLOUDINARY_CLOUD_NAME,
  api_key: process.env.CLOUDINARY_API_KEY,
  api_secret: process.env.CLOUDINARY_API_SECRET,
});

export default cloudinary;

```
* * *

### **How These Files Work Together**

| File | Role in Project |
| --- | --- |
| `tsconfig.json` | Ensures type safety and defines TypeScript behavior. |
| `.eslintrc.json` | Enforces coding standards and catches common errors. |
| `.prettierrc` | Maintains consistent code formatting. |
| `package.json` | Defines dependencies, scripts, and project metadata. |
| `next.config.js` | Customizes Next.js app behavior and plugins. |
| `.env.local` | Stores sensitive data and runtime configuration. |
| `jest.config.js` | Configures testing framework for unit and integration tests. |
| `sentry.*.config.js` | Configures error monitoring and performance tracking. |
| `lighthouserc.js` | Automates performance testing for SEO and speed audits. |
| `lib/cloudinary.js` | Manages media uploads and optimizations with Cloudinary. |

* * *
