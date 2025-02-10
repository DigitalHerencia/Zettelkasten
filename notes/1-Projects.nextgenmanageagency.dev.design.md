---
id: ssmial1emez06ejukkwu3sr
title: design
desc: ''
updated: 1733647076395
created: 1733646537778
---

# Comprehensive Design System 

#### OnlyFans Management Agency Using Tailwind CSS and Shadcn

This guide outlines how to create a scalable and reusable design system for your Next.js + React 19 + TypeScript project using Tailwind CSS for utility-first styling and Shadcn for accessible, prebuilt UI components.

## Design System Goals

**Scalability:** Support multiple user roles (Admin, Creator, Fan).

**Consistency:** Use a unified style for all UI components.

**Reusability:** Modular components that can be reused across dashboards.

**Accessibility:** Ensure all components meet accessibility standards.

**Customization:** Extend Tailwind's utility classes and Shadcn components to match your branding.

### Step 1: Setup Tailwind CSS and Shadcn

- Install Tailwind CSS

```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init

```

- Update tailwind.config.js:

```javascript
const { fontFamily } = require("tailwindcss/defaultTheme");

module.exports = {
  content: [
    "./pages/**/*.{js,ts,jsx,tsx}",
    "./components/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {
      fontFamily: {
        sans: ["Inter", ...fontFamily.sans],
      },
      colors: {
        primary: "#1E90FF", // Blue for branding
        secondary: "#FF69B4", // Pink for highlights
        background: "#F9FAFB", // Light gray for backgrounds
      },
    },
  },
  plugins: [],
};

```

Add Tailwind's base styles in globals.css:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### **Install Shadcn**

1. Install Shadcn:

```bash
npx shadcn init

```

2. Add Shadcn components to your project:

```bash
npx shadcn add button card modal input form table

```
3. Add Shadcn components to your tailwind.config.js:

```javascript
module.exports = {
  plugins: [require("@shadcn/ui/plugin")],
};
```

### Step 2: Define the Design System

#### 1. Color Palette
| Color     | Use Case                           |
|-----------|------------------------------------|
| primary   | Buttons, links, and accents        |
| secondary | Highlights and alerts              |
| background| Page backgrounds                   |
| gray-100  | Card backgrounds                   |
| gray-700  | Text for headings                  |

#### 2. Typography
| Font Weight   | Use Case                   |
|---------------|----------------------------|
| font-light    | Secondary text             |
| font-normal   | Body text                  |
| font-semibold | Section headings           |
| font-bold     | Titles and emphasized text |

### Step 3: Build Core Components

#### 1. Buttons

- Use the Shadcn Button component for primary and secondary actions.

```tsx
import { Button } from "shadcn";

export default function AppButton({ label, variant }: { label: string; variant: "primary" | "secondary" }) {
  return (
    <Button
      className={`${
        variant === "primary"
          ? "bg-primary text-white hover:bg-blue-600"
          : "bg-secondary text-white hover:bg-pink-600"
      } px-4 py-2 rounded-md`}
    >
      {label}
    </Button>
  );
}
```

#### 2. Cards

- Reusable card component for dashboard sections.

```tsx
import { Card } from "shadcn";

export default function DashboardCard({ title, content }: { title: string; content: string }) {
  return (
    <Card className="p-4 bg-gray-100 shadow-md rounded-lg">
      <h3 className="text-lg font-semibold text-gray-700">{title}</h3>
      <p className="text-sm text-gray-600">{content}</p>
    </Card>
  );
}
```

#### 3. Modal

- Use modals for admin coaching or fan feedback.

```tsx
import { Modal } from "shadcn";

export default function FeedbackModal({ isOpen, onClose }: { isOpen: boolean; onClose: () => void }) {
  return (
    <Modal open={isOpen} onClose={onClose}>
      <Modal.Header>
        <h2 className="text-xl font-bold">Submit Feedback</h2>
      </Modal.Header>
      <Modal.Body>
        <textarea className="w-full h-32 p-2 border rounded" placeholder="Enter your feedback"></textarea>
      </Modal.Body>
      <Modal.Footer>
        <button onClick={onClose} className="bg-gray-500 text-white px-4 py-2 rounded">
          Cancel
        </button>
        <button className="bg-primary text-white px-4 py-2 rounded">Submit</button>
      </Modal.Footer>
    </Modal>
  );
}
```

#### 4. Navigation Bar

- A responsive navigation bar for Admin, Creators, and Fans.

```tsx
import { useUser } from "@auth0/nextjs-auth0";

export default function Navbar() {
  const { user } = useUser();

  return (
    <nav className="bg-background shadow p-4">
      <div className="container mx-auto flex justify-between items-center">
        <h1 className="text-xl font-bold text-primary">OnlyFans Management</h1>
        <ul className="flex space-x-4">
          <li>
            <a href="/dashboard" className="text-gray-700 hover:text-primary">
              Dashboard
            </a>
          </li>
          <li>
            <a href="/profile" className="text-gray-700 hover:text-primary">
              Profile
            </a>
          </li>
          {user ? (
            <li>
              <a href="/api/auth/logout" className="text-red-500 hover:text-red-700">
                Logout
              </a>
            </li>
          ) : (
            <li>
              <a href="/api/auth/login" className="text-primary hover:text-blue-700">
                Login
              </a>
            </li>
          )}
        </ul>
      </div>
    </nav>
  );
}
```

#### 5. Tables

Use tables for analytics and metrics.

```tsx
import { Table, TableRow, TableCell } from "shadcn";

export default function MetricsTable({ data }: { data: { name: string; views: number; likes: number }[] }) {
  return (
    <Table className="w-full border border-gray-200 rounded">
      <thead className="bg-gray-100">
        <TableRow>
          <TableCell>Name</TableCell>
          <TableCell>Views</TableCell>
          <TableCell>Likes</TableCell>
        </TableRow>
      </thead>
      <tbody>
        {data.map((row, index) => (
          <TableRow key={index} className="border-t">
            <TableCell>{row.name}</TableCell>
            <TableCell>{row.views}</TableCell>
            <TableCell>{row.likes}</TableCell>
          </TableRow>
        ))}
      </tbody>
    </Table>
  );
}
```

### Step 4: Dashboards

#### Admin Dashboard
```tsx
import DashboardCard from "@/components/DashboardCard";

export default function AdminDashboard() {
  return (
    <div className="p-6 space-y-4">
      <DashboardCard title="Active Creators" content="45 creators are currently active." />
      <DashboardCard title="Total Fans" content="1200 fans subscribed to various creators." />
      <DashboardCard title="Monthly Revenue" content="$25,000 generated this month." />
    </div>
  );
}
```

#### Creator Dashboard
```tsx
import MetricsTable from "@/components/MetricsTable";

const data = [
  { name: "Post 1", views: 120, likes: 45 },
  { name: "Post 2", views: 90, likes: 30 },
];

export default function CreatorDashboard() {
  return (
    <div className="p-6">
      <h2 className="text-2xl font-bold mb-4">Your Content Metrics</h2>
      <MetricsTable data={data} />
    </div>
  );
}
```

#### Fan Dashboard
```tsx
export default function FanDashboard() {
  return (
    <div className="p-6">
      <h2 className="text-2xl font-bold">Your Subscriptions</h2>
      <ul className="space-y-4">
        <li className="p-4 bg-gray-100 rounded shadow">
          Subscribed to <strong>Creator A</strong>. Plan: <em>Premium</em>
        </li>
        <li className="p-4 bg-gray-100 rounded shadow">
          Subscribed to <strong>Creator B</strong>. Plan: <em>Basic</em>
        </li>
      </ul>
    </div>
  );
}
```

### Next Steps

- **Extend the Design System**: Add more components (e.g., tabs, progress bars, dropdowns). Customize Shadcn components for consistent branding.
- **Theming**: Use Tailwind’s theme configuration for dark mode or custom themes.
- **Testing**: Write tests for components with Jest and React Testing Library.