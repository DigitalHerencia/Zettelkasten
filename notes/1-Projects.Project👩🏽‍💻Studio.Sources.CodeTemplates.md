---
id: e3v57im8fu0aua2iq61tvai
title: CodeTemplates
desc: ''
updated: 1742878591263
created: 1742878550254
---
# Code Templates

## Directory Tree

Below is an example of a project structure and some code templates that meet your requirements. In this example, we’re building a blog using Next.js 15 with the app router. The CRUD operations are implemented as server actions in the lib/actions folder, while the API routes in the app/api folders simply call those actions.

```plaintext
my-blog/
├── app/
│   ├── api/
│   │   ├── posts/
│   │   │   └── route.ts         // Handles GET & POST requests for posts
│   │   └── posts/
│   │       └── [id]/
│   │           └── route.ts     // Handles PUT & DELETE for a specific post
│   ├── layout.tsx             // Root layout (includes Clerk provider)
│   ├── page.tsx               // Home page: renders blog list & form
│   └── clerk-provider.tsx     // (Optional) Custom Clerk provider wrapper
├── lib/
│   ├── actions/
│   │   └── posts.ts           // Server actions for CRUD operations
│   └── db/
│       └── mongoose.ts        // Mongoose connection logic
├── models/
│   └── Post.ts                // Mongoose model for blog posts
├── utils/
│   └── postSchema.ts          // Zod schema for validating post data
├── components/
│   ├── PostList.tsx           // Client component to display posts
│   └── PostForm.tsx           // Client component for post submission
├── styles/
│   └── globals.css            // Tailwind CSS imports & global styles
├── .eslintrc.js
├── .prettierrc
├── next.config.js
├── package.json
├── tsconfig.json
└── tailwind.config.js
```

## Templates

1. Mongoose Connection

- File: lib/db/mongoose.ts
  - This file establishes a connection to MongoDB using Mongoose.

```typescript
import mongoose from 'mongoose';

if (!global.mongoose) {
  global.mongoose = { conn: null, promise: null };
}

const MONGODB_URI = process.env.MONGODB_URI || '';

if (!MONGODB_URI) {
  throw new Error('Please define the MONGODB_URI environment variable');
}

export async function connectToDatabase() {
  if (global.mongoose.conn) {
    return global.mongoose.conn;
  }
  if (!global.mongoose.promise) {
    global.mongoose.promise = mongoose.connect(MONGODB_URI).then((mongoose) => mongoose);
  }
  global.mongoose.conn = await global.mongoose.promise;
  return global.mongoose.conn;
}

```

2. Mongoose Model for Post

- File: models/Post.ts

```typescript
import mongoose, { Schema, Document } from 'mongoose';

export interface IPost extends Document {
  title: string;
  content: string;
  createdAt: Date;
  updatedAt: Date;
}

const PostSchema: Schema = new Schema(
  {
    title: { type: String, required: true },
    content: { type: String, required: true },
  },
  { timestamps: true }
);

export default mongoose.models.Post || mongoose.model<IPost>('Post', PostSchema);

```

3. Zod Schema for Post Validation

- File: utils/postSchema.ts

```typescript
import { z } from 'zod';

export const postSchema = z.object({
  title: z.string().min(1, { message: 'Title is required' }),
  content: z.string().min(1, { message: 'Content is required' }),
});

```

4. Server Actions for CRUD Operations

- File: lib/actions/posts.ts

```typescript
import Post from '@/models/Post';
import { postSchema } from '@/utils/postSchema';
import { connectToDatabase } from '@/lib/db/mongoose';

// Ensure database connection before performing any action
async function init() {
  await connectToDatabase();
}

// Create a new post
export async function createPost(data: unknown) {
  await init();
  const parsed = postSchema.parse(data);
  const post = new Post(parsed);
  return await post.save();
}

// Retrieve all posts
export async function getPosts() {
  await init();
  return await Post.find();
}

// Update an existing post
export async function updatePost(id: string, data: unknown) {
  await init();
  const parsed = postSchema.partial().parse(data);
  return await Post.findByIdAndUpdate(id, parsed, { new: true });
}

// Delete a post
export async function deletePost(id: string) {
  await init();
  return await Post.findByIdAndDelete(id);
}

```

5. API Routes

- File: app/api/posts/route.ts
  - a. Posts Collection Route (GET & POST)

```typescript
import { NextResponse } from 'next/server';
import { createPost, getPosts } from '@/lib/actions/posts';

export async function GET() {
  try {
    const posts = await getPosts();
    return NextResponse.json(posts);
  } catch (error) {
    return NextResponse.error();
  }
}

export async function POST(request: Request) {
  try {
    const data = await request.json();
    const post = await createPost(data);
    return NextResponse.json(post);
  } catch (error) {
    return NextResponse.error();
  }
}

```

- File: app/api/posts/[id]/route.ts
  - b. Single Post Route (PUT & DELETE)

```typescript
import { NextResponse } from 'next/server';
import { updatePost, deletePost } from '@/lib/actions/posts';

export async function PUT(
  request: Request,
  { params }: { params: { id: string } }
) {
  try {
    const data = await request.json();
    const post = await updatePost(params.id, data);
    return NextResponse.json(post);
  } catch (error) {
    return NextResponse.error();
  }
}

export async function DELETE(
  request: Request,
  { params }: { params: { id: string } }
) {
  try {
    await deletePost(params.id);
    return NextResponse.json({ message: 'Post deleted' });
  } catch (error) {
    return NextResponse.error();
  }
}

```

6. Root Layout with Clerk Provider

- File: app/layout.tsx

```tsx
import '../styles/globals.css';
import { ClerkProvider } from '@clerk/nextjs';

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en">
      <body>
        <ClerkProvider>{children}</ClerkProvider>
      </body>
    </html>
  );
}

```

7. Home Page

- File: app/page.tsx

```tsx
import PostList from '@/components/PostList';
import PostForm from '@/components/PostForm';

export default function Home() {
  return (
    <div className="container mx-auto p-4 space-y-6">
      <h1 className="text-2xl font-bold">My Blog</h1>
      <PostForm />
      <PostList />
    </div>
  );
}

```

8. Client Components

- File: components/PostForm.tsx
  - a. PostForm Component

```tsx
'use client';
import { useState } from 'react';

export default function PostForm() {
  const [title, setTitle] = useState('');
  const [content, setContent] = useState('');

  async function handleSubmit(e: React.FormEvent) {
    e.preventDefault();
    await fetch('/api/posts', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ title, content }),
    });
    setTitle('');
    setContent('');
  }

  return (
    <form onSubmit={handleSubmit} className="space-y-4">
      <input
        type="text"
        placeholder="Title"
        value={title}
        onChange={(e) => setTitle(e.target.value)}
        className="border p-2 w-full"
      />
      <textarea
        placeholder="Content"
        value={content}
        onChange={(e) => setContent(e.target.value)}
        className="border p-2 w-full"
      />
      <button type="submit" className="bg-blue-500 text-white px-4 py-2">
        Create Post
      </button>
    </form>
  );
}

```

- File: components/PostList.tsx
  - b. PostList Component

```tsx
'use client';
import useSWR from 'swr';

const fetcher = (url: string) => fetch(url).then((res) => res.json());

export default function PostList() {
  const { data, error } = useSWR('/api/posts', fetcher);

  if (error) return <div>Error loading posts.</div>;
  if (!data) return <div>Loading...</div>;

  return (
    <ul className="space-y-4">
      {data.map((post: any) => (
        <li key={post._id} className="border p-4 rounded">
          <h2 className="font-bold text-lg">{post.title}</h2>
          <p>{post.content}</p>
        </li>
      ))}
    </ul>
  );
}

```

9. Configuration Files

- File: next.config.js
  - next.config.js

```javascript
/** @type {import('next').NextConfig} */
const nextConfig = {
  experimental: {
    appDir: true,
  },
  reactStrictMode: true,
};

module.exports = nextConfig;

```

- File: tsconfig.json
  - tsconfig.json

```json
{
  "compilerOptions": {
    "target": "es5",
    "lib": ["dom", "dom.iterable", "esnext"],
    "allowJs": true,
    "skipLibCheck": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "noEmit": true,
    "esModuleInterop": true,
    "module": "esnext",
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "jsx": "preserve",
    "incremental": true
  },
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx"],
  "exclude": ["node_modules"]
}

```

- File: tailwind.config.js
  - tailwind.config.js

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./app/**/*.{js,ts,jsx,tsx}",
    "./components/**/*.{js,ts,jsx,tsx}"
  ],
  theme: {
    extend: {},
  },
  plugins: [],
};

```

- File: .eslintrc.js
  - .eslintrc.js

```javascript
module.exports = {
  root: true,
  parser: '@typescript-eslint/parser',
  plugins: ['@typescript-eslint', 'react'],
  extends: [
    'eslint:recommended',
    'plugin:@typescript-eslint/recommended',
    'plugin:react/recommended',
    'next/core-web-vitals'
  ],
  rules: {
    // Customize your ESLint rules here
  },
};

```

- File: .prettierrc
  - .prettierrc

```json
{
  "semi": true,
  "singleQuote": true,
  "printWidth": 80,
  "tabWidth": 2,
  "trailingComma": "es5"
}

```

## Final Notes

#### Server Actions: 

The CRUD operations are encapsulated as functions in lib/actions/posts.ts. This ensures that your API routes remain thin controllers that simply call these actions.

#### API Routes: 

In the app router, the collection-level route (/api/posts/route.ts) handles GET and POST while the dynamic route (/api/posts/[id]/route.ts) manages updates and deletions.

#### Tech Stack Integration: 

This setup includes Next.js (with the new app directory), React, TypeScript, Tailwind CSS, and integrates with Clerk for authentication. Mongoose, Zod, ESLint, and Prettier ensure that your data layer, validation, and code quality are all maintained.