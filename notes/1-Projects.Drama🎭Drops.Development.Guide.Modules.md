---
id: jkx8n9fwk67wkc41mxgput5
title: Modules
desc: ''
updated: 1736656682807
created: 1736647613679
---

# Development Guide

To develop **"Drama Drops"** as a Next.js 15 web application tailored for the **Gadsden Panthers**, utilizing the App Router, React 19, Shadcn UI for design, and integrating MongoDB with Prisma and Auth0 (including Instagram login), follow this comprehensive guide.
___

### **1\. Project Initialization**

1.  **Set Up Next.js 15 with TypeScript**: Ensure you have Node.js installed. Then, create a new Next.js project:
    
    
    ```
    npx create-next-app@latest drama-drops --typescript
    cd drama-drops

    ```
    
2.  **Install Required Dependencies**: Add necessary packages for Prisma, Shadcn UI, and Auth0:
    
    ```
    npm install @prisma/client @auth0/nextjs-auth0 axios
    npm install -D prisma
    
    
    ```
    
3.  **Initialize Prisma**: Set up Prisma in your project:
    
    ```
    npx prisma init
    ```
    
    This command creates a `prisma` directory with a `schema.prisma` file and a `.env` file for environment variables.
    
4.  **Configure MongoDB Connection**:
    
    -   **Set Up MongoDB Atlas**: Create a free cluster on [MongoDB Atlas](https://www.mongodb.com/atlas/database) and obtain the connection string.
    -   **Update `.env`**: Replace the placeholder in `.env` with your MongoDB connection string:
        
      ```
      DATABASE_URL="mongodb+srv://&lt;username&gt;:&lt;password&gt;@cluster.mongodb.net/drama-drops?retryWrites=true&amp;w=majority"
      
      ```
        

___

### **2\. Database Modeling with Prisma**

Define your data models in `prisma/schema.prisma` to represent users, posts, and reactions:

```
provider = "mongodb"
url      = env("DATABASE_URL")
}

generator client {
  provider = "prisma-client-js"
}

model User {
  id            String   @id @default(auto()) @map("_id") @db.ObjectId
  name          String
  email         String   @unique
  instagramId   String?  @unique
  posts         Post[]
  reactions     Reaction[]
}

model Post {
  id            String     @id @default(auto()) @map("_id") @db.ObjectId
  content       String
  tags          String[]
  createdAt     DateTime   @default(now())
  author        User       @relation(fields: [authorId], references: [id])
  authorId      String     @db.ObjectId
  reactions     Reaction[]
}

model Reaction {
  id            String     @id @default(auto()) @map("_id") @db.ObjectId
  type          String
  user          User       @relation(fields: [userId], references: [id])
  userId        String     @db.ObjectId
  post          Post       @relation(fields: [postId], references: [id])
  postId        String     @db.ObjectId
}

```

After defining the schema, generate the Prisma client:

```
npx prisma generate

```

___

### **3\. Authentication with Auth0 and Instagram Login**

1.  **Set Up Auth0 Application**:
    
    -   **Create Application**: In the [Auth0 Dashboard](https://auth0.com/), create a new Regular Web Application.
    -   **Configure Callbacks**: Set `http://localhost:3000/api/auth/callback` as the Allowed Callback URL and `http://localhost:3000` as the Allowed Logout URL.
2.  **Enable Instagram Social Connection**:
    
    -   **Configure Instagram**: In Auth0, navigate to **Connections** > **Social**, enable Instagram, and provide the necessary Client ID and Secret from the [Meta for Developers Console](https://developers.facebook.com/).
3.  **Configure Auth0 in Next.js**:
    
    -   **Install Auth0 Package**:
        
        ```
        npm install @auth0/nextjs-auth0
        
        ```
        
    -   **Create Auth API Route**: In `app/api/auth/[...auth0]/route.ts`, set up the Auth0 handler:
        
        ```
        import { handleAuth } from '@auth0/nextjs-auth0';
        
        export const GET = handleAuth();
        export const POST = handleAuth();
        </code></div></div>
        
        ```
        
    -   **Update Environment Variables**: Add Auth0 configuration to `.env`:
        
        ```
        AUTH0_SECRET=your_auth0_secret
        AUTH0_BASE_URL=http://localhost:3000
        AUTH0_ISSUER_BASE_URL=https://your-domain.auth0.com
        AUTH0_CLIENT_ID=your_client_id
        AUTH0_CLIENT_SECRET=your_client_secret
        
        ```
        
4.  **Protect Application Routes**:
    
    -   **Wrap Application with Auth0 Provider**: In `app/layout.tsx`, wrap your application with the Auth0 provider:
        
        ```
        import UserProvider from '@auth0/nextjs-auth0';

        export default function RootLayout({ children }) {
          return (
            <html lang="en">
              <body>
                <UserProvider>
                  {children}
                </UserProvider>
              </body>
            </html>
          );
        }
        
        ```
        
    -   **Secure Pages**: Use the `withPageAuthRequired` HOC to protect pages:
        
        ```
        import { withPageAuthRequired } from '@auth0/nextjs-auth0';

        function Dashboard() {
          return (
            <div>
              {/* Dashboard content */}
            </div>
          );
        }

        export default withPageAuthRequired(Dashboard);
        
        ```
        

___

### **4\. Implementing Shadcn UI for Design**

1.  **Install Shadcn UI Components**: Follow the Shadcn UI installation guide to set up the component library in your project.
    
2.  **Customize Theme for Gadsden Panthers**:
    
    -   **Define Custom Theme**: Create a theme file (e.g., `app/theme.ts`) and customize it with Gadsden Panthers' colors and branding elements.
    -   **Apply Theme**: Wrap your application with the ThemeProvider in `app/layout.tsx`:
        
        ```
        import { ThemeProvider } from 'shadcn-ui';
        import theme from './theme';
        
        export default function RootLayout({ children }) {
          return (

        ```
