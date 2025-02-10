---
id: ba2dw9xraoxpsuvhck4o3no
title: CommentedExplanation
desc: ''
updated: 1733473857945
created: 1733376647218
---

### 1. tsconfig.json: TypeScript Configuration

```json
{
  "compilerOptions": {
    "target": "esnext", // Target latest JS features
    "module": "esnext", // Use ES modules
    "jsx": "preserve", // JSX format for React
    "strict": true, // Enable strict type checking
    "moduleResolution": "node", // Node module resolution
    "baseUrl": ".", // Base directory
    "paths": { // Path aliases for cleaner imports
      "@/components/*": ["components/*"],
      "@/lib/*": ["lib/*"],
      "@/styles/*": ["styles/*"]
    }
  },
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx"], // Files to include
  "exclude": ["node_modules"] // Exclude unnecessary files
}

```

***Customization:***

- Update paths with additional directories as your project grows.

### 2. .env.local: Environment Variables

```plaintext
AUTH0_SECRET=your_auth0_secret
AUTH0_BASE_URL=http://localhost:3000
AUTH0_ISSUER_BASE_URL=https://your-auth0-domain.us.auth0.com
AUTH0_CLIENT_ID=your_auth0_client_id
AUTH0_CLIENT_SECRET=your_auth0_client_secret

DATABASE_URL=mongodb+srv://username:password@cluster.mongodb.net/mydatabase
NEXTAUTH_SECRET=your_nextauth_secret

SENTRY_DSN=your_sentry_dsn
STRIPE_SECRET_KEY=your_stripe_secret
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret

```

***Customization:***

- Replace placeholders with actual secrets for your environment. Never commit this file to source control.

### 3. prisma/schema.prisma: Prisma Schema

```prisma
generator client {
  provider = "prisma-client-js" // Generates Prisma client for TypeScript
}

datasource db {
  provider = "mongodb" // Connects to MongoDB
  url      = env("DATABASE_URL") // Uses the DATABASE_URL from .env.local
}

model User {
  id        String   @id @default(auto()) @map("_id") @db.ObjectId
  name      String
  email     String   @unique
  image     String?
  createdAt DateTime @default(now())
}

```

***Customization:***

- Add models as needed (e.g., Post, Comment) and run npx prisma migrate dev to apply changes.

### 4. lib/prisma.ts: Prisma Client

```typescript
import { PrismaClient } from "@prisma/client";

const globalForPrisma = global as unknown as { prisma: PrismaClient };

export const prisma =
  globalForPrisma.prisma ||
  new PrismaClient({
    log: ['query'], // Log database queries for debugging
  });

if (process.env.NODE_ENV !== 'production') globalForPrisma.prisma = prisma;

export default prisma;

```

***Customization:***

- Adjust log options for production to reduce verbosity.

### 5. pages/api/auth/[...auth0].ts: Auth0 Integration

```typescript
import { handleAuth } from "@auth0/nextjs-auth0";

export default handleAuth();

```

***Customization:***

- This default implementation handles login, logout, and callback. Add custom API routes for roles or permissions if needed.

### 6. pages/_app.tsx: Application Wrapper

```typescript
import { AppProps } from "next/app";
import { SessionProvider } from "next-auth/react";
import { ThemeProvider } from "@/lib/theme"; // Custom theme provider
import "@/styles/globals.css";

export default function MyApp({ Component, pageProps }: AppProps) {
  return (
    <SessionProvider session={pageProps.session}>
      <ThemeProvider>
        <Component {...pageProps} />
      </ThemeProvider>
    </SessionProvider>
  );
}

```

***Customization:***

- Add additional context providers or wrappers as your app scales.

### 7. pages/api/example-endpoint.ts: Example API Route

```typescript
import { NextApiRequest, NextApiResponse } from "next";
import prisma from "@/lib/prisma";

export default async function handler(req: NextApiRequest, res: NextApiResponse) {
  if (req.method === "GET") {
    const users = await prisma.user.findMany();
    res.status(200).json(users);
  } else {
    res.setHeader("Allow", ["GET"]);
    res.status(405).end(`Method ${req.method} Not Allowed`);
  }
}

```

***Customization:***

- Add CRUD operations and authentication checks as needed.

### 8. components/Button.tsx: Example Shadcn Component

```typescript
import { Button } from "shadcn";

export default function CustomButton() {
  return (
    <Button
      className="bg-blue-500 hover:bg-blue-600 text-white"
      onClick={() => alert("Button clicked!")}
    >
      Click Me
    </Button>
  );
}

```

***Customization:***

- Use Shadcn components and extend styles with Tailwind CSS as needed.

### 9. lib/cloudinary.ts: Cloudinary Integration

```typescript
import { v2 as cloudinary } from "cloudinary";

cloudinary.config({
  cloud_name: process.env.CLOUDINARY_CLOUD_NAME,
  api_key: process.env.CLOUDINARY_API_KEY,
  api_secret: process.env.CLOUDINARY_API_SECRET,
});

export default cloudinary;

```

***Customization:***

- Use this to handle media uploads and transformations.

### 10. .eslintrc.json: ESLint Configuration

```json
{
  "env": {
    "browser": true,
    "es2021": true
  },
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:react/recommended",
    "prettier"
  ],
  "parser": "@typescript-eslint/parser",
  "plugins": ["@typescript-eslint", "react", "prettier"],
  "rules": {
    "prettier/prettier": "error",
    "react/react-in-jsx-scope": "off"
  }
}

```

***Customization:***

- Add or override specific rules for your project's needs.

### 11. .prettierrc: Prettier Configuration

```json
{
  "semi": true,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "all"
}

```

***Customization:***

- Adjust formatting preferences like tab width or quote styles.

### 12. next.config.js: Next.js Configuration

```javascript
const nextConfig = {
  reactStrictMode: true,
  images: {
    domains: ["res.cloudinary.com"], // Allow images from Cloudinary
  },
  env: {
    AUTH0_BASE_URL: process.env.AUTH0_BASE_URL,
  },
};

module.exports = nextConfig;

```

***Customization***:

- Add additional configurations like headers, redirects, or plugins.

## Practice Task

- ***Challenge:*** Set up the above templates in your project.
- ***Bonus:*** Extend them to include additional features like Stripe for payments or Sentry for monitoring.
