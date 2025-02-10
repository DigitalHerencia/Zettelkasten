---
id: k4pao6mpqkskacrhjb9jhz7
title: BuildingBlocks
desc: ''
updated: 1733461872385
created: 1733461599538
---

## 1. Navigation Links Template

#### This template centralizes navigation links to maintain consistency across the app.

``` ts
// lib/navigationLinks.ts
const navigationLinks = {
  admin: [
    { name: "Dashboard", href: "/admin/dashboard" },
    { name: "Creators", href: "/admin/creators" },
    { name: "Analytics", href: "/admin/analytics" },
  ],
  creator: [
    { name: "Dashboard", href: "/creators/[id]/dashboard" },
    { name: "My Posts", href: "/creators/[id]/posts" },
    { name: "Subscriptions", href: "/creators/[id]/subscriptions" },
  ],
  fan: [
    { name: "Dashboard", href: "/fans/[id]/dashboard" },
    { name: "Subscriptions", href: "/fans/[id]/subscriptions" },
  ],
};

export default navigationLinks;

```

## 2. Custom Hook

#### Reusable hook for fetching data with error handling and loading states.

``` ts
// hooks/useFetch.ts
import { useState, useEffect } from "react";

export const useFetch = (url: string) => {
  const [data, setData] = useState(null);
  const [error, setError] = useState<string | null>(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    setLoading(true);
    fetch(url)
      .then((response) => response.json())
      .then((result) => setData(result))
      .catch((err) => setError(err.message))
      .finally(() => setLoading(false));
  }, [url]);

  return { data, error, loading };
};

```

## 3. Error Boundary

#### Catch runtime errors to prevent the app from crashing.

``` tsx
// components/shared/ErrorBoundary.tsx
import { Component, ReactNode } from "react";

type Props = {
  children: ReactNode;
};

type State = {
  hasError: boolean;
};

export default class ErrorBoundary extends Component<Props, State> {
  state: State = { hasError: false };

  static getDerivedStateFromError() {
    return { hasError: true };
  }

  componentDidCatch(error: Error) {
    console.error("Error caught by ErrorBoundary:", error);
  }

  render() {
    if (this.state.hasError) {
      return <div>Something went wrong. Please try again later.</div>;
    }
    return this.props.children;
  }
}

```

## 4. Modal for User Interaction

#### A modal template for reusable confirmation dialogs or input forms.

``` tsx
// components/shared/Modal.tsx
type ModalProps = {
  isOpen: boolean;
  onClose: () => void;
  children: React.ReactNode;
};

export default function Modal({ isOpen, onClose, children }: ModalProps) {
  if (!isOpen) return null;

  return (
    <div className="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50">
      <div className="bg-white rounded p-6 w-96">
        {children}
        <button
          onClick={onClose}
          className="mt-4 bg-red-500 text-white py-2 px-4 rounded"
        >
          Close
        </button>
      </div>
    </div>
  );
}

```

## 5. Form Validation

#### A template for a form using React Hook Form with validation.

``` tsx
// components/forms/FeedbackForm.tsx
import { useForm } from "react-hook-form";

type FeedbackFormData = {
  message: string;
};

export default function FeedbackForm({ onSubmit }: { onSubmit: (data: FeedbackFormData) => void }) {
  const { register, handleSubmit, formState: { errors } } = useForm<FeedbackFormData>();

  return (
    <form onSubmit={handleSubmit(onSubmit)} className="space-y-4">
      <textarea
        {...register("message", { required: "Message is required" })}
        className="w-full p-2 border rounded"
        placeholder="Enter your feedback"
      />
      {errors.message && <p className="text-red-500">{errors.message.message}</p>}
      <button type="submit" className="bg-primary text-white py-2 px-4 rounded">
        Submit Feedback
      </button>
    </form>
  );
}

```

## 6. Protected Route

#### Template for securing pages based on user roles.

``` tsx
// components/auth/ProtectedRoute.tsx
import { useUser } from "@auth0/nextjs-auth0";
import { useRouter } from "next/router";

export default function ProtectedRoute({ children, role }: { children: React.ReactNode; role: string }) {
  const { user } = useUser();
  const router = useRouter();

  if (!user) {
    router.push("/api/auth/login");
    return null;
  }

  if (user.role !== role) {
    router.push("/403");
    return null;
  }

  return <>{children}</>;
}

```

## 7. Pagination Controls

#### Reusable pagination component.

``` tsx
// components/shared/Pagination.tsx
type PaginationProps = {
  currentPage: number;
  totalPages: number;
  onPageChange: (page: number) => void;
};

export default function Pagination({ currentPage, totalPages, onPageChange }: PaginationProps) {
  return (
    <div className="flex items-center justify-center space-x-4">
      <button
        onClick={() => onPageChange(currentPage - 1)}
        disabled={currentPage === 1}
        className="px-4 py-2 bg-gray-200 rounded disabled:opacity-50"
      >
        Previous
      </button>
      <span>
        Page {currentPage} of {totalPages}
      </span>
      <button
        onClick={() => onPageChange(currentPage + 1)}
        disabled={currentPage === totalPages}
        className="px-4 py-2 bg-gray-200 rounded disabled:opacity-50"
      >
        Next
      </button>
    </div>
  );
}

```

## 8. API Request Wrapper

#### Reusable API request handler.

``` ts
// lib/apiRequest.ts
export async function apiRequest<T>(url: string, options?: RequestInit): Promise<T> {
  const response = await fetch(url, options);

  if (!response.ok) {
    throw new Error(`HTTP Error: ${response.status}`);
  }

  return response.json();
}

```

## 9. Notification System

#### A simple toast notification system.

``` tsx
// components/shared/Toast.tsx
import { useState, useEffect } from "react";

type ToastProps = {
  message: string;
  duration?: number;
};

export default function Toast({ message, duration = 3000 }: ToastProps) {
  const [visible, setVisible] = useState(true);

  useEffect(() => {
    const timer = setTimeout(() => setVisible(false), duration);
    return () => clearTimeout(timer);
  }, [duration]);

  if (!visible) return null;

  return (
    <div className="fixed bottom-4 right-4 bg-black text-white py-2 px-4 rounded shadow">
      {message}
    </div>
  );
}

```

## 10. 404 Page

#### A custom 404 page to enhance user experience.

``` tsx
// pages/404.tsx
export default function NotFound() {
  return (
    <div className="min-h-screen flex items-center justify-center bg-gray-100">
      <div className="text-center">
        <h1 className="text-4xl font-bold">404</h1>
        <p className="text-lg">Page Not Found</p>
        <a href="/" className="text-primary mt-4 block">
          Go Back Home
        </a>
      </div>
    </div>
  );
}
