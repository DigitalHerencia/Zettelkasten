---
id: nwg7p79amlfv8ijqvcepv05
title: prisma
desc: ''
updated: 1733563031968
created: 1733340641453
---

### Lesson 12: **Advanced Database Management with Prisma ORM**

*(Simplify database interaction with a modern ORM for TypeScript and JavaScript.)*

* * *

#### What is Prisma?

- **Definition**: A next-generation ORM (Object-Relational Mapper) that simplifies database queries, schema management, and migrations.
- **Key Features**:
    - **Type Safety**: Automatically generates TypeScript types.
    - **Migrations**: Handles database schema changes.
    - **Multi-Database Support**: Works with PostgreSQL, MySQL, MongoDB, SQLite, and more.

* * *

#### Why Use Prisma?

| Feature | Benefit |
| --- | --- |
| **Type Safety** | Reduces runtime errors by ensuring queries match schema. |
| **Auto-Generated Queries** | Faster development with boilerplate code generation. |
| **Readable Schema** | Database schema is defined in a declarative file. |
| **Support for MongoDB** | Works seamlessly with MongoDB Atlas. |

* * *

### Step 1: Set Up Prisma in Your Project

1. **Install Prisma**:

```bash
   npm install prisma --save-devnpm install @prisma/client

```

2. **Initialize Prisma**:

```bash
   npx prisma init

```
   
 - This creates a `prisma/` folder with a `schema.prisma` file for defining your database schema.

* * *

### Step 2: Configure Prisma for MongoDB

1. **Update the `prisma/schema.prisma` File**:

```prisma
generator client { provider = "prisma-client-js"} 
datasource db { provider = "mongodb" url = env("MONGODB_URI")} 
model Post {
  id       String   @id @default(auto()) @map("_id") @db.ObjectId
  title    String
  content  String
  createdAt DateTime @default(now())
}

```
- **Model**: Represents a MongoDB collection.
- **Field Annotations**:
- `@id`: Defines the primary key.
- `@db.ObjectId`: Marks the `id` field as a MongoDB ObjectId.

2. **Update `.env.local` with Your MongoDB URI**:

``` plaintext
MONGODB_URI=your_mongo_connection_string

```

* * *

### Step 3: Generate Prisma Client

- Run the following command to generate the Prisma client:

        bashCopy codenpx prisma generate
- This creates the Prisma client, which allows you to interact with your database.

* * *

### Step 4: Use Prisma in a Next.js API Route

1. **Set Up Prisma Client**:

    - Create a `lib/prisma.js` file:

            javascriptCopy codeimport { PrismaClient } from '@prisma/client'; const prisma = new PrismaClient();export default prisma;
2. **Fetch Data with Prisma**:

    - Add a file `pages/api/posts.js`:

            javascriptCopy codeimport prisma from '@/lib/prisma'; export default async function handler(req, res) { if (req.method === 'GET') { const posts = await prisma.post.findMany(); res.status(200).json(posts); }}
3. **Use the API in Your Frontend**:

    - Update `pages/index.js` to fetch data:

            javascriptCopy codeimport { useEffect, useState } from 'react'; export default function Home() { const [posts, setPosts] = useState([]); useEffect(() => { fetch('/api/posts') .then((res) => res.json()) .then((data) => setPosts(data)); }, []); return ( <div className="min-h-screen p-6 bg-gray-100"> <h1 className="text-3xl font-bold">Posts</h1> <ul> {posts.map((post) => ( <li key={post.id} className="py-2"> <h2 className="text-xl font-semibold">{post.title}</h2> <p>{post.content}</p> </li> ))} </ul> </div> );}

* * *

### Step 5: Insert Data with Prisma

1. **Handle POST Requests**:

    - Update `pages/api/posts.js`:

            javascriptCopy codeif (req.method === 'POST') { const { title, content } = req.body; const post = await prisma.post.create({ data: { title, content }, }); res.status(201).json(post);}
2. **Add a Form to Create Posts**:

    - Update `pages/index.js`:

            javascriptCopy codeconst handleSubmit = async (e) => { e.preventDefault(); const title = e.target.title.value; const content = e.target.content.value; await fetch('/api/posts', { method: 'POST', headers: { 'Content-Type': 'application/json' }, body: JSON.stringify({ title, content }), });}; return ( <form onSubmit={handleSubmit} className="space-y-4"> <input name="title" type="text" placeholder="Title" className="block border rounded px-4 py-2" /> <textarea name="content" placeholder="Content" className="block border rounded px-4 py-2" /> <button type="submit" className="px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600" > Submit </button> </form>);

* * *

### Prisma Query Examples

| Query | Code |
| --- | --- |
| **Find All Posts** | `prisma.post.findMany()` |
| **Find by ID** | `prisma.post.findUnique({ where: { id: "someId" } })` |
| **Create a Post** | `prisma.post.create({ data: { title: "Title", content: "Content" } })` |
| **Update a Post** | `prisma.post.update({ where: { id: "someId" }, data: { title: "Updated Title" } })` |
| **Delete a Post** | `prisma.post.delete({ where: { id: "someId" } })` |

* * *

### Practice Task

1. **Challenge**: Add a "Delete" button to each post.

    - Implement a DELETE API route.
    - Use `fetch` to call the DELETE API from the frontend.
2. **Bonus**: Add sorting and pagination to the posts list.

* * *

### Advanced Features

1. **Relations**: Add related models like `User` and associate them with posts.
2. **Migrations**: Use `prisma migrate dev` to apply schema changes.
3. **Seeding Data**: Add initial data using a seed script.

* * *

### Resources

- Prisma Documentation
- Prisma MongoDB Integration
- Learn interactively: [Prisma Quick Start](https://www.youtube.com/watch?v=RebA5J-rlwg)