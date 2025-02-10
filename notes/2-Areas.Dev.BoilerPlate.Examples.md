---
id: hoypm3q9rwmpkrpk6cnilpf
title: Examples
desc: ''
updated: 1733644289951
created: 1733377868630
---


## **Project Structure**

```
my-nextjs-project/
├── components/
├── pages/
│   ├── api/
│   │   ├── auth/[...auth0].ts
│   │   ├── prisma-handler.ts
│   │   ├── example-endpoint.ts
│   ├── _app.tsx
│   ├── index.tsx
├── prisma/
│   ├── schema.prisma
├── lib/
│   ├── prisma.ts
│   ├── auth0.ts
│   ├── cloudinary.ts
├── styles/
├── public/
├── .env.local
├── next.config.js
├── tsconfig.json
├── .eslintrc.json
├── .prettierrc
├── package.json
└── README.md

```
* * *

### **1. `tsconfig.json`: TypeScript Configuration**

```json
{
  "compilerOptions": {
    "target": "esnext",
    "module": "esnext",
    "jsx": "preserve",
    "strict": true,
    "moduleResolution": "node",
    "baseUrl": ".",
    "paths": {
      "@/components/*": ["components/*"],
      "@/lib/*": ["lib/*"],
      "@/styles/*": ["styles/*"]
    }
  },
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx"],
  "exclude": ["node_modules"]
}

```

> 
> **Customization:**  
> Update `paths` with additional directories as your project grows.

* * *

### **2. `.env.local`: Environment Variables**

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
> 
> **Customization:**  
> Replace placeholders with actual secrets for your environment. Never commit this file to source control.

* * *

### **3. `prisma/schema.prisma`: Prisma Schema**

```prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "mongodb"
  url      = env("DATABASE_URL")
}

model User {
  id        String   @id @default(auto()) @map("_id") @db.ObjectId
  name      String
  email     String   @unique
  image     String?
  createdAt DateTime @default(now())
}

```
> 
> **Customization:**  
> Add models as needed (e.g., Post, Comment) and run `npx prisma migrate dev` to apply changes.

* * *

### **4. `lib/prisma.ts`: Prisma Client**

```typescript
import { PrismaClient } from "@prisma/client";

const globalForPrisma = global as unknown as {
  prisma: PrismaClient;
};

export const prisma =
  globalForPrisma.prisma ||
  new PrismaClient({
    log: ["query"], // Log database queries for debugging
  });

if (process.env.NODE_ENV !== "production")
  globalForPrisma.prisma = prisma;

export default prisma;

```
> 
> **Customization:**  
> Adjust `log` options for production to reduce verbosity.

* * *

### **5. `pages/api/auth/[...auth0].ts`: Auth0 Integration**

```typescript
import { handleAuth } from "@auth0/nextjs-auth0";

export default handleAuth();

```
> 
> **Customization:**  
> This default implementation handles login, logout, and callback. Add custom API routes for roles or permissions if needed.

* * *

### **6. `pages/_app.tsx`: Application Wrapper**

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
> 
> **Customization:**  
> Add additional context providers or wrappers as your app scales.

* * *

### **7. `pages/api/example-endpoint.ts`: Example API Route**

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
> 
> **Customization:**  
> Add CRUD operations and authentication checks as needed.

* * *

### **8. `components/Button.tsx`: Example Shadcn Component**

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
> 
> **Customization:**  
> Use Shadcn components and extend styles with Tailwind CSS as needed.

* * *

### **9. `lib/cloudinary.ts`: Cloudinary Integration**

```typescript
import { v2 as cloudinary } from "cloudinary";

cloudinary.config({
  cloud_name: process.env.CLOUDINARY_CLOUD_NAME,
  api_key: process.env.CLOUDINARY_API_KEY,
  api_secret: process.env.CLOUDINARY_API_SECRET,
});

export default cloudinary;

```
> 
> **Customization:**  
> Use this to handle media uploads and transformations.

* * *

### **10. `.eslintrc.json`: ESLint Configuration**

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
> 
> **Customization:**  
> Add or override specific rules for your project's needs.

* * *

### **11. `.prettierrc`: Prettier Configuration**

```json
{
  "semi": true,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "all"
}

```
> 
> **Customization:**  
> Adjust formatting preferences like tab width or quote styles.

* * *

### **12. `next.config.js`: Next.js Configuration**

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
> 
> **Customization:**  
> Add additional configurations like headers, redirects, or plugins.

* * *

### **13. `lib/auth0.ts`: Auth0 Helper Functions**

```typescript
import { getSession, withApiAuthRequired } from "@auth0/nextjs-auth0";

/**
 * Helper to retrieve the authenticated user's session.
 */
export const getUserSession = async (req: any, res: any) => {
  const session = getSession(req, res);
  if (!session) {
    throw new Error("User not authenticated");
  }
  return session.user;
};

/**
 * Middleware to protect API routes.
 */
export const requireAuth = withApiAuthRequired((req, res) => {
  // This can be used to enforce protected APIs
  return req;
});

```
> 
> **Use:** Retrieve session or enforce authentication on specific API routes.

* * *

### **14. `prisma/seed.ts`: Seed Script**

```typescript

import { PrismaClient } from "@prisma/client";
const prisma = new PrismaClient();

async function main() {
  await prisma.user.createMany({
    data: [
      { name: "John Doe", email: "john@example.com" },
      { name: "Jane Smith", email: "jane@example.com" },
    ],
  });
  console.log("Database seeded!");
}

main()
  .catch((e) => {
    console.error(e);
    process.exit(1);
  })
  .finally(() => {
    prisma.$disconnect();
  });

```

> 
> **Use:** Run this script with `npx prisma db seed` to seed initial data.

* * *

### **15. `components/Navbar.tsx`: Example Navigation Bar**

```typescript
import Link from "next/link";
import { useUser } from "@auth0/nextjs-auth0";

export default function Navbar() {
  const { user } = useUser();

  return (
    <nav className="p-4 bg-gray-800 text-white">
      <div className="container mx-auto flex justify-between items-center">
        <Link href="/">
          <a className="text-xl font-bold">MyApp</a>
        </Link>
        <div>
          {user ? (
            <>
              <span className="mr-4">Hello, {user.name}</span>
              <a href="/api/auth/logout" className="px-4 py-2 bg-red-500 rounded">
                Logout
              </a>
            </>
          ) : (
            <a href="/api/auth/login" className="px-4 py-2 bg-blue-500 rounded">
              Login
            </a>
          )}
        </div>
      </div>
    </nav>
  );
}

```
> 
> **Use:** Customize navigation links and include conditional logic for authenticated users.

* * *

### **16. `pages/dashboard.tsx`: Protected Page**

```typescript
import { withPageAuthRequired } from "@auth0/nextjs-auth0";

function Dashboard({ user }: any) {
  return (
    <div className="p-6">
      <h1 className="text-2xl font-bold">Welcome, {user.name}!</h1>
      <p>Your email: {user.email}</p>
    </div>
  );
}

export const getServerSideProps = withPageAuthRequired();

export default Dashboard;

> 
> **Use:** Use `withPageAuthRequired` to enforce authentication for pages.

* * *

### **17. `lib/validate.ts`: Input Validation Utility**

``typescript
  import * as yup from "yup";

export const userSchema = yup.object({
  name: yup.string().required("Name is required").min(3, "Name must be at least 3 characters"),
  email: yup.string().email("Invalid email format").required("Email is required"),
});

/**
 * Validates data using a Yup schema.
 */
export const validateInput = async (schema: any, data: any) => {
  try {
    await schema.validate(data, { abortEarly: false });
    return { valid: true };
  } catch (error: any) {
    return { valid: false, errors: error.inner };
  }
};

```
> 
> **Use:** Centralize validation logic for user input (e.g., forms or APIs).

* * *

### **18. `pages/api/upload.ts`: File Upload API**

```typescript
import { NextApiRequest, NextApiResponse } from "next";
import cloudinary from "@/lib/cloudinary";

export default async function handler(req: NextApiRequest, res: NextApiResponse) {
  if (req.method === "POST") {
    const { file } = req.body;

    try {
      const uploadResponse = await cloudinary.uploader.upload(file, {
        folder: "uploads",
      });
      res.status(200).json({ url: uploadResponse.secure_url });
    } catch (error) {
      res.status(500).json({ error: "File upload failed" });
    }
  } else {
    res.setHeader("Allow", ["POST"]);
    res.status(405).end(`Method ${req.method} Not Allowed`);
  }
}

```
> 
> **Use:** Handle file uploads securely with Cloudinary.

* * *

### **19. `lib/react-query.ts`: React Query Configuration**

```typescript 
import { QueryClient } from "@tanstack/react-query";

export const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      refetchOnWindowFocus: false, // Prevent auto-refetch on focus
      staleTime: 1000 * 60 * 5, // Cache queries for 5 minutes
    },
  },
});

```
> 
> **Use:** Set up centralized configuration for React Query.

* * *

### **20. `jest.setup.js`: Jest Setup**

```javascript
import "@testing-library/jest-dom/extend-expect";

// Mock global variables like fetch if needed
global.fetch = jest.fn(() =>
  Promise.resolve({
    json: () => Promise.resolve([]),
  })
);
```
> 
> **Use:** Include this file for setting up Jest and mocking global APIs.

* * *

### **21. `pages/api/webhook.ts`: Webhook Handler (e.g., Stripe)**

```typescript
   import { NextApiRequest, NextApiResponse } from "next";
import { buffer } from "micro";

export const config = {
  api: {
    bodyParser: false, // Stripe needs raw body for webhook validation
  },
};

export default async function handler(req: NextApiRequest, res: NextApiResponse) {
  if (req.method === "POST") {
    const buf = await buffer(req);
    const signature = req.headers["stripe-signature"];

    try {
      // Use Stripe SDK to verify webhook
      const event = stripe.webhooks.constructEvent(buf, signature, process.env.STRIPE_WEBHOOK_SECRET);

      // Handle event
      if (event.type === "checkout.session.completed") {
        console.log("Payment Successful");
      }

      res.status(200).json({ received: true });
    } catch (error) {
      res.status(400).send(`Webhook Error: ${error.message}`);
    }
  } else {
    res.setHeader("Allow", ["POST"]);
    res.status(405).end(`Method ${req.method} Not Allowed`);
  }
}

```
> 
> **Use:** Replace Stripe with your desired webhook source.

* * *

### **22. `components/Modal.tsx`: Shadcn Modal**

```typescript
    
   import { Modal } from "shadcn";

type ModalProps = {
  isOpen: boolean;
  onClose: () => void;
  title: string;
  children: React.ReactNode;
};

export default function CustomModal({ isOpen, onClose, title, children }: ModalProps) {
  return (
    <Modal open={isOpen} onClose={onClose}>
      <Modal.Header>
        <h2 className="text-lg font-bold">{title}</h2>
      </Modal.Header>
      <Modal.Body>{children}</Modal.Body>
      <Modal.Footer>
        <button onClick={onClose} className="bg-gray-500 px-4 py-2 text-white rounded">
          Close
        </button>
      </Modal.Footer>
    </Modal>
  );
}

```
> 
> **Use:** Modular, reusable modal component styled with Shadcn.
