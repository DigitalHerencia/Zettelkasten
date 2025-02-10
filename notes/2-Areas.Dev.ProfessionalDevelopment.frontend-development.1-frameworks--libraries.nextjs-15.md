---
id: ujnrff7pgdksdjbse9eif2u
title: nextjs-15
desc: ''
updated: 1733339772300
created: 1733339683219
---

### Lesson 2: **Next.js Basics**

*(Enhancing React with server-side rendering, routing, and SEO optimizations.)*

* * *

#### What is Next.js?

- **Definition**: A React-based framework for building web applications with features like:
    - **Server-Side Rendering (SSR)**: Pages are pre-rendered on the server for better performance and SEO.
    - **Static Site Generation (SSG)**: Pages are generated at build time and served as static files.
    - **File-based Routing**: Automatic routes based on the file structure.
    - Built-in **API routes** for backend functionality.

* * *

#### Why Next.js?

| Feature | Benefit |
| --- | --- |
| **Server-Side Rendering** | Improves SEO and faster initial page loads. |
| **Static Site Generation** | Optimized for blogs, landing pages, and e-commerce sites. |
| **API Routes** | Build serverless functions alongside frontend code. |
| **Automatic Routing** | No need for third-party libraries like React Router. |
| **Optimized Images** | Built-in image optimization with `next/image`. |

* * *

#### Interactive Activity: Create Your First Next.js App

1. **Setup**:
    - Run the following commands in your terminal:

            bashCopy codenpx create-next-app@latest my-next-appcd my-next-appnpm run dev
    - Open `http://localhost:3000` in your browser. You should see the default Next.js welcome page.

* * *

#### Code Example: Basic Page with Routing

1. **Add a New Page**:
    - Create a file `about.js` in the `pages/` directory.
    - Add this code:

            jsxCopy codeexport default function About() { return ( <div> <h1>About Us</h1> <p>Welcome to the about page of our Next.js app!</p> </div> );}
    - Save and navigate to `http://localhost:3000/about`. You’ve created your first route!

* * *

#### File-Based Routing Overview:

| File Location | URL Path |
| --- | --- |
| `pages/index.js` | `/` (homepage) |
| `pages/about.js` | `/about` |
| `pages/blog/post.js` | `/blog/post` |

* * *

#### Add Navigation with `Link`:

- Update `index.js` to include links to navigate between pages:

        jsxCopy codeimport Link from 'next/link'; export default function Home() { return ( <div> <h1>Welcome to Next.js</h1> <nav> <Link href="/about">About Us</Link> </nav> </div> );}

* * *

#### Diagram: Next.js Rendering Methods

    plaintextCopy codeClient-Side Rendering (CSR) <-- Traditional React apps |Server-Side Rendering (SSR) <-- Pre-rendered on each request |Static Site Generation (SSG) <-- Pre-rendered at build time

* * *

#### Practice:

1. **Task**: Create a new page `contact.js` and add a form with fields for name, email, and a message.
2. **Challenge**: Link it to the homepage using `Link` and test navigation.

* * *

#### Resources:

- Next.js Official Docs
- Free interactive course: [Next.js Crash Course on FreeCodeCamp](https://www.youtube.com/watch?v=mTz0GXj8NN0)