---
id: n41285st4xdzrsfkx2h1t23
title: nextjs-api-routes
desc: ''
updated: 1733340842921
created: 1733340816758
---

### Lesson 15: **Custom API Development with Next.js API Routes**

*(Learn to create powerful backend functionality directly within your Next.js app.)*

* * *

#### What Are Next.js API Routes?

- **Definition**: Built-in serverless functions that allow you to define backend API endpoints within your Next.js app.
- **Key Features**:
    - Reside inside the `pages/api/` directory.
    - Fully integrated with Next.js.
    - Can handle requests like any backend framework (e.g., Express.js).

* * *

#### Why Use Next.js API Routes?

| Feature | Benefit |
| --- | --- |
| **Serverless** | Scales automatically with serverless infrastructure. |
| **Integrated** | Share code and context between frontend and backend. |
| **Rapid Development** | No need for external servers or frameworks. |
| **Flexible** | Supports REST and GraphQL. |

* * *

### Basic Example: Hello World API

1. **Create an API Route**:

    - Add a file `pages/api/hello.js`:

            javascriptCopy codeexport default function handler(req, res) { res.status(200).json({ message: 'Hello, World!' });}
2. **Test the API**:

    - Start your development server and visit `http://localhost:3000/api/hello` in your browser.
    - You should see:

            jsonCopy code{ "message": "Hello, World!" }

* * *

### Key Concepts of Next.js API Routes

| Concept | Description |
| --- | --- |
| **Request Object (`req`)** | Contains HTTP method, headers, body, etc. |
| **Response Object (`res`)** | Used to send a response to the client. |
| **Dynamic Routes** | Create endpoints with parameters (e.g., `/api/user/[id].js`). |
| **Middleware Support** | Integrate authentication, validation, or logging. |

* * *

### Example: CRUD API for Posts

1. **Set Up a Database (Optional)**:

    - Use MongoDB or Prisma (from previous lessons) for storing posts.
    - Alternatively, use a simple in-memory array for demonstration.
2. **Create API Route for Posts**:

    - Add a file `pages/api/posts.js`:

            javascriptCopy codelet posts = []; export default function handler(req, res) { if (req.method === 'GET') { res.status(200).json(posts); } else if (req.method === 'POST') { const { title, content } = req.body; const newPost = { id: Date.now(), title, content }; posts.push(newPost); res.status(201).json(newPost); } else { res.setHeader('Allow', ['GET', 'POST']); res.status(405).end(`Method ${req.method} Not Allowed`); }}
3. **Test GET and POST Requests**:

    - Use a tool like **Postman**or the browser to test:
        - `GET /api/posts`: Fetch all posts.
        - `POST /api/posts`: Add a new post with a JSON body like:

                jsonCopy code{ "title": "First Post", "content": "This is my first post." }

* * *

### Example: Dynamic API Routes

1. **Add a Dynamic Route**:

    - Add a file `pages/api/posts/[id].js`:

            javascriptCopy codeexport default function handler(req, res) { const { id } = req.query; if (req.method === 'GET') { const post = posts.find((p) => p.id === parseInt(id)); if (post) { res.status(200).json(post); } else { res.status(404).json({ error: 'Post not found' }); } } else if (req.method === 'DELETE') { posts = posts.filter((p) => p.id !== parseInt(id)); res.status(204).end(); } else { res.setHeader('Allow', ['GET', 'DELETE']); res.status(405).end(`Method ${req.method} Not Allowed`); }}
2. **Test the Dynamic Routes**:

    - `GET /api/posts/1`: Fetch a specific post.
    - `DELETE /api/posts/1`: Delete a specific post.

* * *

### Advanced Features

#### Middleware for Validation

1. **Add Validation with Middleware**:
    - Create a validation helper:

            javascriptCopy codeexport function validateRequest(req, res, schema) { const { error } = schema.validate(req.body); if (error) { res.status(400).json({ error: error.details[0].message }); return false; } return true;}
    - Use it in `pages/api/posts.js`:

            javascriptCopy codeimport Joi from 'joi';import { validateRequest } from '@/lib/validate'; const schema = Joi.object({ title: Joi.string().required(), content: Joi.string().required(),}); if (req.method === 'POST') { if (!validateRequest(req, res, schema)) return; // Continue with POST logic}

#### Authentication with Middleware

1. **Protect Routes**:
    - Add middleware to verify authentication:

            javascriptCopy codeimport { getSession } from 'next-auth/react'; export async function handler(req, res) { const session = await getSession({ req }); if (!session) { res.status(401).json({ error: 'Unauthorized' }); return; } // Continue with API logic}

* * *

### Practice Task

1. **Challenge**: Create a full CRUD API for managing users.
    - Fields: `id`, `name`, `email`.
    - Include validation for required fields.
2. **Bonus**: Add middleware to authenticate requests.

* * *

### Advanced Use Cases

1. **GraphQL API**:
    - Use a library like Apollo Server to build a GraphQL API in your Next.js app.
2. **Real-Time Updates**:
    - Integrate with a service like **Pusher** or **WebSocket** for real-time data.
3. **Error Logging**:
    - Use services like **Sentry** to log and track API errors.

* * *

### Resources

- Next.js API Routes Documentation
- [RESTful API Design](https://restfulapi.net/)
- Learn interactively: [Next.js API Tutorial](https://www.youtube.com/watch?v=ZXmQ7fuxDV8)