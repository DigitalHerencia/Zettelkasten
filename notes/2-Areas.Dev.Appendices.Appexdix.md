---
id: vqim5kht2sr2s35qtzmgt2x
title: Appexdix
desc: ''
updated: 1733382075785
created: 1733380998899
---

# Appendix

## 1. Core JavaScript/TypeScript Syntax Essentials

### Variables

```typescript
const name: string = "John"; // Constant variable, immutable
let age: number = 30;       // Mutable variable

```

### Functions

```typescript
function greet(name: string): string {
  return `Hello, ${name}!`;
}

const add = (a: number, b: number): number => a + b; // Arrow function

```

### Classes

```typescript
class User {
  private name: string;

  constructor(name: string) {
    this.name = name;
  }

  getName(): string {
    return this.name;
  }
}

```

### TypeScript Types and Interfaces

```typescript
type UserType = {
  id: string;
  name: string;
  email: string;
};

interface AdminType extends UserType {
  isAdmin: boolean;
}

```

## 2. React Essentials

### Basic Component

```typescript
import React from "react";

type GreetingProps = {
  name: string;
};

const Greeting: React.FC<GreetingProps> = ({ name }) => {
  return <h1>Hello, {name}!</h1>;
};

export default Greeting;

```

### State Management

```typescript
import React, { useState } from "react";

const Counter: React.FC = () => {
  const [count, setCount] = useState<number>(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
};

export default Counter;

```

### Props Example

```typescript
type ButtonProps = {
  label: string;
  onClick: () => void;
};

const Button: React.FC<ButtonProps> = ({ label, onClick }) => (
  <button onClick={onClick}>{label}</button>
);

```

## 3. Next.js Specific

### Server-Side Rendering (SSR)

```typescript
import { GetServerSideProps } from "next";

type Props = {
  user: { name: string };
};

export default function Home({ user }: Props) {
  return <h1>Welcome, {user.name}!</h1>;
}

export const getServerSideProps: GetServerSideProps = async () => {
  return { props: { user: { name: "John Doe" } } };
};

```

### Static Site Generation (SSG)

```typescript
import { GetStaticProps } from "next";

type Props = {
  posts: { id: string; title: string }[];
};

export default function Posts({ posts }: Props) {
  return (
    <ul>
      {posts.map((post) => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  );
}

export const getStaticProps: GetStaticProps = async () => {
  const posts = [{ id: "1", title: "First Post" }]; // Replace with fetch logic
  return { props: { posts } };
};

```

### API Route

```typescript
import { NextApiRequest, NextApiResponse } from "next";

export default function handler(req: NextApiRequest, res: NextApiResponse) {
  if (req.method === "GET") {
    res.status(200).json({ message: "Hello, API!" });
  } else {
    res.status(405).json({ error: "Method Not Allowed" });
  }
}

```

## 4. Prisma + MongoDB Essentials

### Prisma Schema Example

```prisma
model User {
  id    String  @id @default(auto()) @map("_id") @db.ObjectId
  name  String
  email String  @unique
  posts Post[]
}

model Post {
  id      String   @id @default(auto()) @map("_id") @db.ObjectId
  title   String
  content String
  userId  String
  user    User     @relation(fields: [userId], references: [id])
}

```

### Prisma Client Usage

```typescript
import { PrismaClient } from "@prisma/client";

const prisma = new PrismaClient();

export async function createUser() {
  const user = await prisma.user.create({
    data: { name: "John Doe", email: "john@example.com" },
  });
  console.log(user);
}

```

## 5. Auth0 Essentials

### API Route for Auth0

```typescript
import { handleAuth } from "@auth0/nextjs-auth0";

export default handleAuth();

```

### User Profile Retrieval

```typescript
import { useUser } from "@auth0/nextjs-auth0";

export default function Profile() {
  const { user } = useUser();

  return user ? (
    <div>
      <h1>{user.name}</h1>
      <p>{user.email}</p>
    </div>
  ) : (
    <p>Loading...</p>
  );
}

```

## 6. Styling (Tailwind + Shadcn)

### Tailwind Example

```tsx
export default function Button() {
  return
    <button 
      className="bg-blue-500 text-white px-4 py-2 rounded">
         Click Me
    </button>;
}

```

### Shadcn Example

```tsx
import { Button } from "shadcn";

export default function ShadButton() {
  return
    <Button 
      className="bg-blue-500 text-white">
        Shadcn Button
    </Button>;
}

```

## 7. Deployment Commands (Vercel)

### Local Testing

```bash
npm run dev

```

### Build for Production

```bash
npm run build

```

### Deploy to Vercel

```bash
vercel deploy

```

## 8. Testing (Jest + React Testing Library)

###Jest Example

```typescript
test("adds 1 + 2 to equal 3", () => {
  expect(1 + 2).toBe(3);
  }
);

```

### React Testing Library

```typescript
import { render, screen } from "@testing-library/react";
import "@testing-library/jest-dom";
import Counter from "./Counter";

test("renders counter", () => {
  render(<Counter />);
  expect(screen.getByText("Count: 0")).toBeInTheDocument();
  }
);

```

## 9. React Query Example

### Fetch Data

```typescript
import { useQuery } from "@tanstack/react-query";

const fetchUsers = async () => {
  const res = await fetch("/api/users");
  return res.json();
};

export default function Users() {
  const { data, isLoading } = useQuery(["users"], fetchUsers);

  if (isLoading) return <p>Loading...</p>;

  return (
    <ul>
      {data.map((user: any) => (
        <li key={user.id}>{user.name}</li>
        )
       )
      }
    </ul>
  );
}

```

## 10. Commands and Utilities

### CLI Commands

- Initialize Next.js:

```bash
npx create-next-app@latest my-app --typescript

```

- Add Prisma:

```bash
npm install @prisma/client
npx prisma init

```

- Add Auth0:

```bash
npm install @auth0/nextjs-auth0

```

- Utility Functions

```typescript
export function debounce(func: Function, delay: number) {
  let timer: NodeJS.Timeout;
  return (...args: any[]) => {
    clearTimeout(timer);
    timer = setTimeout(() => func(...args), delay);
  };
}

```