---
id: 32twpo48p03g7b2k1vcf85t
title: nextauthjs
desc: ''
updated: 1733340727803
created: 1733340698586
---

### Lesson 13: **Authentication with NextAuth.js**

*(Securely authenticate users in your Next.js application.)*

* * *

#### What is NextAuth.js?

- **Definition**: A flexible and secure authentication library for Next.js that supports multiple providers (e.g., Google, GitHub, Email, etc.).
- **Key Features**:
    - **Built-in Authentication Pages**: Prebuilt UI for sign-in and sign-out.
    - **Multiple Providers**: Google, GitHub, Twitter, Email, and more.
    - **JWT Support**: JSON Web Tokens for session management.
    - **Database Integration**: Store users in a database (optional).

* * *

#### Why Use NextAuth.js?

| Feature | Benefit |
| --- | --- |
| **Ease of Integration** | Quick setup with minimal code. |
| **Secure by Default** | Prebuilt security best practices. |
| **Flexible Providers** | Add social, email, or custom authentication easily. |
| **Session Management** | Easily manage sessions and user data. |

* * *

### Step 1: Install NextAuth.js

1. Install NextAuth.js and its dependencies:

        bashCopy codenpm install next-auth

* * *

### Step 2: Create an API Route for Authentication

1. Add a new API route `pages/api/auth/[...nextauth].js`:

        javascriptCopy codeimport NextAuth from 'next-auth';import GoogleProvider from 'next-auth/providers/google'; export default NextAuth({ providers: [ GoogleProvider({ clientId: process.env.GOOGLE_CLIENT_ID, clientSecret: process.env.GOOGLE_CLIENT_SECRET, }), ], secret: process.env.NEXTAUTH_SECRET,});
2. **Environment Variables**:

    - Add the following to `.env.local`:

            plaintextCopy codeGOOGLE_CLIENT_ID=your_google_client_idGOOGLE_CLIENT_SECRET=your_google_client_secretNEXTAUTH_SECRET=your_random_secret
    - Replace `your_google_client_id` and `your_google_client_secret` with values from the Google Cloud Console.

* * *

### Step 3: Add Authentication UI

1. **Use the `SignIn` and `SignOut` Functions**:

    - Update `pages/index.js`:

            javascriptCopy codeimport { useSession, signIn, signOut } from 'next-auth/react'; export default function Home() { const { data: session } = useSession(); if (!session) { return ( <div className="min-h-screen flex flex-col items-center justify-center"> <h1 className="text-2xl">Welcome! Please sign in.</h1> <button className="px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600" onClick={() => signIn('google')} > Sign In with Google </button> </div> ); } return ( <div className="min-h-screen flex flex-col items-center justify-center"> <h1 className="text-2xl">Welcome, {session.user.name}!</h1> <img src={session.user.image} alt={session.user.name} className="w-16 h-16 rounded-full" /> <p>{session.user.email}</p> <button className="mt-4 px-4 py-2 bg-red-500 text-white rounded hover:bg-red-600" onClick={() => signOut()} > Sign Out </button> </div> );}
2. **Wrap Your App with the Session Provider**:

    - Update `_app.js`:

            javascriptCopy codeimport { SessionProvider } from 'next-auth/react'; export default function App({ Component, pageProps }) { return ( <SessionProvider session={pageProps.session}> <Component {...pageProps} /> </SessionProvider> );}

* * *

### Step 4: Protect Pages with Middleware

1. **Protect Pages Based on Authentication**:

    - Add a middleware to redirect unauthenticated users:

        - Create a file `middleware.js`:

                javascriptCopy codeimport { withAuth } from 'next-auth/middleware'; export default withAuth({ pages: { signIn: '/auth/signin', },});
    - Protect specific routes by adding a `matcher`:

            javascriptCopy codeexport const config = { matcher: ['/protected-page/:path*'],};
2. **Optional**: Redirect Unauthenticated Users Manually:

    - Add this check in any page:

            javascriptCopy codeimport { useSession } from 'next-auth/react';import { useRouter } from 'next/router'; export default function ProtectedPage() { const { data: session, status } = useSession(); const router = useRouter(); if (status === 'loading') { return <p>Loading...</p>; } if (!session) { router.push('/auth/signin'); return null; } return <h1>Welcome to the protected page, {session.user.name}!</h1>;}

* * *

### Step 5: Add a Database for Persistent Sessions

1. **Install Prisma Adapter**:

        bashCopy codenpm install @next-auth/prisma-adapter
2. **Add Prisma Models**:

    - Update `prisma/schema.prisma`:

            prismaCopy codemodel Account { id String @id @default(cuid()) userId String type String provider String providerAccountId String accessToken String? refreshToken String? expiresAt Int? user User @relation(fields: [userId], references: [id])} model User { id String @id @default(cuid()) name String? email String? @unique emailVerified DateTime? image String? accounts Account[]}
3. **Configure the Prisma Adapter**:

    - Update your `[...nextauth].js`:

            javascriptCopy codeimport { PrismaAdapter } from '@next-auth/prisma-adapter';import prisma from '@/lib/prisma'; export default NextAuth({ adapter: PrismaAdapter(prisma), providers: [ // Add your providers here ],});

* * *

### Practice Task

1. **Challenge**: Add a "Dashboard" page that only logged-in users can access.
    - Redirect unauthenticated users to the sign-in page.
2. **Bonus**: Use `useSession` to display user-specific data on the dashboard.

* * *

### Advanced Features

1. **Custom Credentials Provider**:
    - Add a custom username/password authentication method.
2. **Multi-Provider Authentication**:
    - Add GitHub, Twitter, or email authentication alongside Google.
3. **JWT Customization**:
    - Customize JWT tokens to include roles or additional user data.

* * *

### Resources

- NextAuth.js Documentation
- Google Cloud Console
- Learn interactively: [NextAuth.js Video Tutorial](https://www.youtube.com/watch?v=svq4c4zyZGo)