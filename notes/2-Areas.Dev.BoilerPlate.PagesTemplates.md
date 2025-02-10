---
id: nikukom6c6qgqkqef1u1vxr
title: PagesTemplates
desc: ''
updated: 1733378306050
created: 1733378022958
---


# Pages Templates

## # 1. pages/profile.tsx: User Profile Page

- Use: Shows the currently logged-in user's profile information.

```typescript
Copy code
import { withPageAuthRequired } from "@auth0/nextjs-auth0";

export default function Profile({ user }: any) {
  return (
    <div className="p-6">
      <h1 className="text-2xl font-bold">Profile</h1>
      <p>Name: {user.name}</p>
      <p>Email: {user.email}</p>
      {user.picture && <img src={user.picture} alt={user.name} className="rounded-full w-32 h-32 mt-4" />}
    </div>
  );
}
export const getServerSideProps = withPageAuthRequired();
```


## # 2. pages/register.tsx: User Registration Page

- Use: A form to handle user registration. Connect it to your API or Auth0 backend.

```typescript
import { useState } from "react";

export default function Register() {
  const [formData, setFormData] = useState({ name: "", email: "", password: "" });

  const handleSubmit = async (e: React.FormEvent) => {
    e.preventDefault();
    const res = await fetch("/api/register", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(formData),
    });
    const data = await res.json();
    alert(data.message);
  };

  return (
    <form onSubmit={handleSubmit} className="p-6 max-w-md mx-auto">
      <h1 className="text-2xl font-bold mb-4">Register</h1>
      <input
        type="text"
        placeholder="Name"
        value={formData.name}
        onChange={(e) => setFormData({ ...formData, name: e.target.value })}
        className="block w-full mb-2 p-2 border rounded"
      />
      <input
        type="email"
        placeholder="Email"
        value={formData.email}
        onChange={(e) => setFormData({ ...formData, email: e.target.value })}
        className="block w-full mb-2 p-2 border rounded"
      />
      <input
        type="password"
        placeholder="Password"
        value={formData.password}
        onChange={(e) => setFormData({ ...formData, password: e.target.value })}
        className="block w-full mb-4 p-2 border rounded"
      />
      <button type="submit" className="w-full bg-blue-500 text-white py-2 rounded">
        Register
      </button>
    </form>
  );
}

```

## # 3. pages/login.tsx: Login Page

- Use: Allows users to log in and displays their current session if authenticated.

```typescript
import { useUser } from "@auth0/nextjs-auth0";

export default function Login() {
  const { user } = useUser();

  if (user) {
    return (
      <div className="text-center">
        <h1 className="text-2xl">Welcome back, {user.name}!</h1>
        <a href="/api/auth/logout" className="text-blue-500 underline">
          Logout
        </a>
      </div>
    );
  }

  return (
    <div className="text-center">
      <h1 className="text-2xl">Login to Your Account</h1>
      <a href="/api/auth/login" className="text-blue-500 underline">
        Login
      </a>
    </div>
  );
}
```
## # 4. pages/admin.tsx: Admin Dashboard

- Use: Admin-only dashboard, restricting access based on user roles.

```typescript
import { withPageAuthRequired } from "@auth0/nextjs-auth0";

export default function AdminDashboard() {
  return (
    <div className="p-6">
      <h1 className="text-3xl font-bold">Admin Dashboard</h1>
      <p>Manage your application here.</p>
    </div>
  );
}

export const getServerSideProps = withPageAuthRequired({
  getServerSideProps: async ({ req, res }) => {
    const session = await getSession(req, res);

    if (session?.user.email !== "admin@example.com") {
      return { redirect: { destination: "/", permanent: false } };
    }

    return { props: {} };
  },
});

```

## 5. pages/posts/index.tsx: Blog Posts List

- Use: Lists blog posts fetched from a /api/posts endpoint.

```typescript
import { useEffect, useState } from "react";

export default function Posts() {
  const [posts, setPosts] = useState([]);

  useEffect(() => {
    fetch("/api/posts")
      .then((res) => res.json())
      .then((data) => setPosts(data));
  }, []);

  return (
    <div className="p-6">
      <h1 className="text-2xl font-bold">Blog Posts</h1>
      <ul>
        {posts.map((post) => (
          <li key={post.id} className="mb-4">
            <h2 className="text-xl">{post.title}</h2>
            <p>{post.content}</p>
          </li>
        ))}
      </ul>
    </div>
  );
}
```

## 6. pages/posts/id.tsx: Single Post Page

- Use: Displays a single post by ID, fetched from a Prisma database.

```typescript
import { GetServerSideProps } from "next";
import prisma from "@/lib/prisma";

export default function Post({ post }: any) {
  if (!post) {
    return <p>Post not found.</p>;
  }

  return (
    <div className="p-6">
      <h1 className="text-3xl font-bold">{post.title}</h1>
      <p>{post.content}</p>
    </div>
  );
}

export const getServerSideProps: GetServerSideProps = async ({ params }) => {
  const post = await prisma.post.findUnique({
    where: { id: String(params?.id) },
  });

  return {
    props: { post },
  };
};

```

## 7. pages/settings.tsx: User Settings

- Use: Allows users to modify account settings.

```typescript
import { withPageAuthRequired } from "@auth0/nextjs-auth0";

export default function Settings() {
  return (
    <div className="p-6">
      <h1 className="text-2xl font-bold">User Settings</h1>
      <form>
        <label className="block mb-2">
          Email Notifications:
          <input type="checkbox" className="ml-2" />
        </label>
        <button type="submit" className="mt-4 bg-blue-500 text-white py-2 px-4 rounded">
          Save Settings
        </button>
      </form>
    </div>
  );
}

export const getServerSideProps = withPageAuthRequired();
```


## 8. pages/404.tsx: Custom 404 Page

- Use: A custom error page for handling 404s.

```typescript
export default function Custom404() {
  return (
    <div className="text-center p-6">
      <h1 className="text-3xl font-bold">404 - Page Not Found</h1>
      <p>The page you are looking for does not exist.</p>
      <a href="/" className="text-blue-500 underline">
        Go back to the homepage
      </a>
    </div>
  );
}
```


## 9. pages/api/posts/index.ts: API for Blog Posts

- Use: Fetch posts for your blog.

```typescript
import { NextApiRequest, NextApiResponse } from "next";
import prisma from "@/lib/prisma";

export default async function handler(req: NextApiRequest, res: NextApiResponse) {
  if (req.method === "GET") {
    const posts = await prisma.post.findMany();
    res.status(200).json(posts);
  } else {
    res.setHeader("Allow", ["GET"]);
    res.status(405).end(`Method ${req.method} Not Allowed`);
  }
}
```

## 10. pages/contact.tsx: Contact Form

- Use: Collects user inquiries and sends them to a /api/contact endpoint.

```typescript
import { useState } from "react";

export default function Contact() {
  const [formData, setFormData] = useState({ name: "", email: "", message: "" });

  const handleSubmit = async (e: React.FormEvent) => {
    e.preventDefault();
    const res = await fetch("/api/contact", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(formData),
    });
    const data = await res.json();
    alert(data.message);
  };

  return (
    <form onSubmit={handleSubmit} className="p-6 max-w-md mx-auto">
      <h1 className="text-2xl font-bold mb-4">Contact Us</h1>
      <input
        type="text"
        placeholder="Name"
        value={formData.name}
        onChange={(e) => setFormData({ ...formData, name: e.target.value })}
        className="block w-full mb-2 p-2 border rounded"
      />
      <input
        type="email"
        placeholder="Email"
        value={formData.email}
        onChange={(e) => setFormData({ ...formData, email: e.target.value })}
        className="block w-full mb-2 p-2 border rounded"
      />
      <textarea
        placeholder="Message"
        value={formData.message}
        onChange={(e) => setFormData({ ...formData, message: e.target.value })}
        className="block w-full mb-4 p-2 border rounded"
      />
      <button type="submit" className="w-full bg-green-500 text-white py-2 rounded">
        Submit
      </button>
    </form>
  );
}

```

# Practice Task
- **Challenge:** Implement these templates in your project and customize for your needs.
- **Bonus:** Add role-based access (e.g., admin-only pages) and integrate data-fetching libraries like React Query for dynamic updates.
