---
id: 1hh6u53zyfvvntu6zoytoy9
title: react-query
desc: ''
updated: 1733340265543
created: 1733340225801
---

### Lesson 7: **React Query**

*(Efficient data fetching and caching for your applications.)*

* * *

#### What is React Query?

- **Definition**: A powerful library for managing server state in React applications.
- **Why React Query?**
    - Simplifies **data fetching** and **caching**.
    - Automatically **syncs** data with the server.
    - Built-in **stale-while-revalidate** mechanism for optimal performance.
    - Handles **loading**, **error**, and **success** states out of the box.

* * *

#### When to Use React Query?

- You’re fetching data from APIs and need:
    - Automatic caching and refetching.
    - To manage loading/error states easily.
    - Pagination or infinite scrolling.
    - Background updates when data becomes stale.

* * *

#### Installing React Query

1. **Install the Library**:

    - Run:

            bashCopy codenpm install @tanstack/react-query
2. **Set Up the Query Client**:

    - Create a `QueryClient` and wrap your app with the `QueryClientProvider` in `_app.js`:

            javascriptCopy codeimport { QueryClient, QueryClientProvider } from '@tanstack/react-query'; const queryClient = new QueryClient(); export default function App({ Component, pageProps }) { return ( <QueryClientProvider client={queryClient}> <Component {...pageProps} /> </QueryClientProvider> );}

* * *

#### Example: Fetch Data with React Query

1. **Fetching Data from an API**:
    - Replace `pages/index.js` with:

            javascriptCopy codeimport { useQuery } from '@tanstack/react-query'; function fetchPosts() { return fetch('https://jsonplaceholder.typicode.com/posts').then((res) => res.json());} export default function Home() { const { data, isLoading, isError } = useQuery(['posts'], fetchPosts); if (isLoading) return <p>Loading...</p>; if (isError) return <p>Something went wrong!</p>; return ( <div className="min-h-screen p-6 bg-gray-100"> <h1 className="text-3xl font-bold">Posts</h1> <ul> {data.map((post) => ( <li key={post.id} className="py-2"> <h2 className="text-xl font-semibold">{post.title}</h2> <p>{post.body}</p> </li> ))} </ul> </div> );}

* * *

#### React Query's Key Concepts

| Concept | Description |
| --- | --- |
| **`useQuery`** | Fetches data and caches the result. |
| **`useMutation`** | Handles create, update, or delete operations. |
| **`QueryClient`** | Manages the cache and global configuration for React Query. |
| **Key** | Unique identifier for each query to cache and refetch data. |
| **Stale Time** | Time before cached data is considered stale and refetch is triggered. |

* * *

#### Managing Mutations with `useMutation`

1. **Add a Post to the API**:
    - Update `pages/index.js`:

            javascriptCopy codeimport { useMutation, useQueryClient } from '@tanstack/react-query'; function createPost(newPost) { return fetch('https://jsonplaceholder.typicode.com/posts', { method: 'POST', headers: { 'Content-Type': 'application/json' }, body: JSON.stringify(newPost), }).then((res) => res.json());} export default function Home() { const queryClient = useQueryClient(); const mutation = useMutation(createPost, { onSuccess: () => { queryClient.invalidateQueries(['posts']); // Refetch posts }, }); return ( <div className="min-h-screen p-6 bg-gray-100"> <h1 className="text-3xl font-bold">Add a Post</h1> <button className="px-4 py-2 mt-4 text-white bg-blue-500 rounded hover:bg-blue-600" onClick={() => mutation.mutate({ title: 'New Post', body: 'This is a new post.' }) } > Add Post </button> </div> );}

* * *

#### Advanced Use Case: Infinite Scrolling

1. **Fetch Data in Chunks**:
    - Example with infinite scroll:

            javascriptCopy codeimport { useInfiniteQuery } from '@tanstack/react-query'; function fetchPosts({ pageParam = 1 }) { return fetch( `https://jsonplaceholder.typicode.com/posts?_page=${pageParam}&_limit=10` ).then((res) => res.json());} export default function Home() { const { data, fetchNextPage, hasNextPage, isFetchingNextPage } = useInfiniteQuery( ['posts'], fetchPosts, { getNextPageParam: (lastPage, pages) => (lastPage.length ? pages.length + 1 : undefined), } ); return ( <div className="min-h-screen p-6 bg-gray-100"> <h1 className="text-3xl font-bold">Infinite Posts</h1> <ul> {data?.pages.map((page) => page.map((post) => ( <li key={post.id} className="py-2"> <h2 className="text-xl font-semibold">{post.title}</h2> <p>{post.body}</p> </li> )) )} </ul> <button onClick={() => fetchNextPage()} disabled={!hasNextPage || isFetchingNextPage} className="px-4 py-2 mt-4 text-white bg-green-500 rounded hover:bg-green-600" > {isFetchingNextPage ? 'Loading...' : hasNextPage ? 'Load More' : 'No More Posts'} </button> </div> );}

* * *

#### Practice Task

1. **Challenge**: Create a "Users List" page using `useQuery`to fetch users from:
    - API: `https://jsonplaceholder.typicode.com/users`
2. **Bonus**: Add a form to create a new user using `useMutation`.

* * *

#### React Query vs Redux Toolkit

| Feature | React Query | Redux Toolkit |
| --- | --- | --- |
| **Purpose** | Server-state management (data fetching). | Client-state management (UI & app logic). |
| **Caching** | Automatic caching and invalidation. | Manual caching. |
| **Data Fetching** | Built-in support for APIs. | Requires extra setup. |

* * *

#### Resources:

- React Query Docs
- Learn React Query with: [React Query Crash Course](https://www.youtube.com/watch?v=8S4rXP-8m5c)
