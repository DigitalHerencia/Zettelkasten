---
id: 3c06me4g8lnawhw7bqoatpl
title: programming-languages
desc: ''
updated: 1733341756824
created: 1733341714281
---

### Lesson 22: **Using TypeScript in Next.js**

*(Enhance your app with type safety, better code maintainability, and improved developer experience.)*

* * *

#### What is TypeScript?

- **Definition**: A superset of JavaScript that adds static typing, making it easier to catch errors during development.
- **Key Features**:
    - Optional static typing.
    - Supports modern JavaScript features.
    - Integrates seamlessly with React and Next.js.

* * *

#### Why Use TypeScript in Next.js?

| Feature | Benefit |
| --- | --- |
| **Type Safety** | Catch bugs during development, not runtime. |
| **Better IDE Support** | Enhanced autocompletion, refactoring, and navigation. |
| **Scalable Codebase** | Makes it easier to manage large projects. |
| **Integration** | Works out of the box with Next.js. |

* * *

### Step 1: Set Up TypeScript in Your Project

1. **Install TypeScript and Required Dependencies**:

        bashCopy codenpm install --save-dev typescript @types/react @types/node
2. **Run the Dev Server**:

    - Start the development server:

            bashCopy codenpm run dev
    - This generates a `tsconfig.json` file.
3. **Configure `tsconfig.json`** (Optional):

    - Example configuration:

            jsonCopy code{ "compilerOptions": { "target": "esnext", "module": "esnext", "jsx": "preserve", "strict": true, "moduleResolution": "node", "baseUrl": ".", "paths": { "@/components/*": ["components/*"], "@/lib/*": ["lib/*"] } }, "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx"], "exclude": ["node_modules"]}
4. **Rename Files**:

    - Rename all `.js` and `.jsx` files to `.ts` and `.tsx`.

* * *

### Step 2: Adding TypeScript to Components

1. **Basic Functional Component**:

    - Update `pages/index.tsx`:

            tsxCopy codeimport { FC } from 'react'; const Home: FC = () => { return <h1>Hello, TypeScript!</h1>;}; export default Home;
2. **Props with TypeScript**:

    - Define and use props:

            tsxCopy codetype ButtonProps = { label: string; onClick: () => void;}; const Button: FC<ButtonProps> = ({ label, onClick }) => { return ( <button onClick={onClick} className="px-4 py-2 bg-blue-500 text-white rounded"> {label} </button> );}; export default Button;
3. **Use the Component**:

    - Import and use the `Button` component:

            tsxCopy codeimport Button from '@/components/Button'; const Home: FC = () => { const handleClick = () => alert('Button clicked!'); return <Button label="Click Me" onClick={handleClick} />;}; export default Home;

* * *

### Step 3: TypeScript in API Routes

1. **Create a Typed API Route**:
    - Update `pages/api/hello.ts`:

            typescriptCopy codeimport type { NextApiRequest, NextApiResponse } from 'next'; type Data = { message: string;}; export default function handler(req: NextApiRequest, res: NextApiResponse<Data>) { res.status(200).json({ message: 'Hello, TypeScript!' });}

* * *

### Step 4: Using TypeScript with State and Context

1. **Typed State with `useState`**:

    - Example Counter:

            tsxCopy codeimport { useState } from 'react'; const Counter: FC = () => { const [count, setCount] = useState<number>(0); return ( <div> <h1>Count: {count}</h1> <button onClick={() => setCount(count + 1)}>Increment</button> </div> );}; export default Counter;
2. **Using Context**:

    - Create a `ThemeContext`:

            tsxCopy codeimport { createContext, useContext, useState, FC } from 'react'; type Theme = 'light' | 'dark';type ThemeContextType = { theme: Theme; toggleTheme: () => void;}; const ThemeContext = createContext<ThemeContextType | undefined>(undefined); export const ThemeProvider: FC = ({ children }) => { const [theme, setTheme] = useState<Theme>('light'); const toggleTheme = () => setTheme((prev) => (prev === 'light' ? 'dark' : 'light')); return ( <ThemeContext.Provider value={{ theme, toggleTheme }}> {children} </ThemeContext.Provider> );}; export const useTheme = () => { const context = useContext(ThemeContext); if (!context) throw new Error('useTheme must be used within ThemeProvider'); return context;};
    - Use the `ThemeContext` in a Component:

            tsxCopy codeimport { useTheme } from '@/context/ThemeContext'; const ThemeToggle: FC = () => { const { theme, toggleTheme } = useTheme(); return ( <div> <p>Current Theme: {theme}</p> <button onClick={toggleTheme}>Toggle Theme</button> </div> );}; export default ThemeToggle;

* * *

### Step 5: TypeScript in Libraries

1. **Integrate with Axios**:

    - Example of a typed API call:

            typescriptCopy codeimport axios from 'axios'; type User = { id: number; name: string;}; const fetchUsers = async (): Promise<User[]> => { const response = await axios.get('/api/users'); return response.data;};
2. **Use in React Query**:

    - Example:

            tsxCopy codeimport { useQuery } from '@tanstack/react-query'; const fetchUsers = async (): Promise<User[]> => { const response = await fetch('/api/users'); return response.json();}; const Users: FC = () => { const { data, isLoading, error } = useQuery(['users'], fetchUsers); if (isLoading) return <p>Loading...</p>; if (error) return <p>Error loading users</p>; return ( <ul> {data.map((user) => ( <li key={user.id}>{user.name}</li> ))} </ul> );}; export default Users;

* * *

### Best Practices

| Tip | Explanation |
| --- | --- |
| **Enable Strict Mode** | Use `"strict": true` in `tsconfig.json` for better safety. |
| **Use Interfaces** | Prefer interfaces over types for object shapes. |
| **Leverage Generics** | Use generics for reusable components and utilities. |
| **Annotate Early** | Explicitly annotate props, state, and return values. |
| **Refactor Often** | Use TypeScript to simplify and improve your codebase. |

* * *

### Practice Task

1. **Challenge**: Build a typed `TodoList` component.

    - Features:
        - Add and remove todos.
        - Mark todos as complete.
    - Use TypeScript for state, props, and API interactions.
2. **Bonus**: Create a `useLocalStorage` custom hook that is typed for different data types.

* * *

### Advanced Features

1. **Utility Types**:

    - Use built-in utility types like `Partial<T>`, `Pick<T, K>`, and `Omit<T, K>` to simplify complex types.

        typescriptCopy codetype PartialUser = Partial<User>;type UserWithoutId = Omit<User, 'id'>;
2. **Type Guards**:

    - Create custom type guards for better runtime type checking:

            typescriptCopy codeconst isUser = (data: any): data is User => { return 'id' in data && 'name' in data;};
3. **Monorepo Support**:

    - Use TypeScript's `paths` and `references` for shared modules in a monorepo.

* * *

### Resources

- TypeScript Handbook
- Next.js with TypeScript
- Learn interactively: [TypeScript Crash Course](https://www.youtube.com/watch?v=BCg4U1FzODs)