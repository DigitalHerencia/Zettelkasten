---
id: czx5mhza6s9c7h1nsciqvly
title: theme
desc: ''
updated: 1733647113692
created: 1733646554373
---

# Theming with Shadcn and Next.js

Shadcn offers a great foundation for creating **theming systems** in your Next.js project. Combined with **Tailwind CSS**, you can implement dynamic light/dark mode support or even custom themes for branding.

* * *

## **Step 1: Define Your Theme Tokens**

In `tailwind.config.js`, extend the default theme to include your custom colors and tokens for primary, secondary, and background colors.

```javascript
const { fontFamily } = require("tailwindcss/defaultTheme");

module.exports = {
  content: [
    "./pages/**/*.{js,ts,jsx,tsx}",
    "./components/**/*.{js,ts,jsx,tsx}",
    "./app/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {
      fontFamily: {
        sans: ["Inter", ...fontFamily.sans],
      },
      colors: {
        primary: {
          DEFAULT: "#1E90FF", // Default primary blue
          dark: "#1C86EE", // Darker blue
          light: "#ADD8E6", // Lighter blue
        },
        secondary: {
          DEFAULT: "#FF69B4", // Default pink
          dark: "#FF1493", // Darker pink
          light: "#FFB6C1", // Lighter pink
        },
        background: {
          DEFAULT: "#F9FAFB", // Light background
          dark: "#1A202C", // Dark background
        },
        text: {
          DEFAULT: "#1A202C", // Dark text
          light: "#F9FAFB", // Light text
        },
      },
    },
  },
  plugins: [],
};

```

* * *

## **Step 2: Create a Theme Context**

To manage dynamic theming in your app, create a **ThemeContext**.

1. Create a new file: `lib/theme.tsx`.

```tsx
import { createContext, useContext, useState } from "react";

type Theme = "light" | "dark";

const ThemeContext = createContext<{
  theme: Theme;
  toggleTheme: () => void;
}>({
  theme: "light",
  toggleTheme: () => {},
});

export const ThemeProvider = ({ children }: { children: React.ReactNode }) => {
  const [theme, setTheme] = useState<Theme>("light");

  const toggleTheme = () => {
    setTheme((prev) => (prev === "light" ? "dark" : "light"));
  };

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      <div className={theme === "light" ? "theme-light" : "theme-dark"}>{children}</div>
    </ThemeContext.Provider>
  );
};

export const useTheme = () => useContext(ThemeContext);

```

1. Wrap your app with `ThemeProvider` in `_app.tsx`.

```tsx
import { ThemeProvider } from "@/lib/theme";
import "@/styles/globals.css";

export default function App({ Component, pageProps }: any) {
  return (
    <ThemeProvider>
      <Component {...pageProps} />
    </ThemeProvider>
  );
}

```

* * *

## **Step 3: Style Themes in CSS**

Define your light and dark mode styles in `globals.css`.

```css
/* globals.css */
@tailwind base;
@tailwind components;
@tailwind utilities;

/* Light Theme */
.theme-light {
  --color-background: #f9fafb;
  --color-text: #1a202c;
  --color-primary: #1e90ff;
  --color-secondary: #ff69b4;
}

/* Dark Theme */
.theme-dark {
  --color-background: #1a202c;
  --color-text: #f9fafb;
  --color-primary: #1c86ee;
  --color-secondary: #ff1493;
}

/* Apply Theme Variables */
body {
  background-color: var(--color-background);
  color: var(--color-text);
}

a {
  color: var(--color-primary);
}

```

* * *

## **Step 4: Toggle Themes**

Add a theme toggle button to your navigation or header.

```tsx
import { useTheme } from "@/lib/theme";

export default function ThemeToggle() {
  const { theme, toggleTheme } = useTheme();

  return (
    <button
      onClick={toggleTheme}
      className="p-2 rounded border border-gray-300 hover:bg-gray-200 dark:hover:bg-gray-700"
    >
      {theme === "light" ? "Switch to Dark Mode" : "Switch to Light Mode"}
    </button>
  );
}

```

* * *

## **Step 5: Integrate Themes with Shadcn Components**

Shadcn components use Tailwind for styling, so you can dynamically apply themes using your CSS variables.

### Example: Themed Button Component

1. Customize the Shadcn `Button` component.

```tsx
import { useTheme } from "@/lib/theme";

export default function ThemeToggle() {
  const { theme, toggleTheme } = useTheme();

  return (
    <button
      onClick={toggleTheme}
      className="p-2 rounded border border-gray-300 hover:bg-gray-200 dark:hover:bg-gray-700"
    >
      {theme === "light" ? "Switch to Dark Mode" : "Switch to Light Mode"}
    </button>
  );
}

```

### Example: Themed Card Component

1. Customize the Shadcn `Card` component.

```tsx
import { Card as ShadcnCard } from "shadcn";

export default function ThemedCard({ title, content }: { title: string; content: string }) {
  return (
    <ShadcnCard className="p-4 rounded-lg shadow-md bg-background text-text">
      <h2 className="text-lg font-bold">{title}</h2>
      <p className="text-sm">{content}</p>
    </ShadcnCard>
  );
}

```
* * *

## **Step 6: Persist Theme Preference**

To save the user's theme preference, use **localStorage**.

1. Update `ThemeProvider` in `lib/theme.tsx`:

```tsx
import { createContext, useContext, useEffect, useState } from "react";

type Theme = "light" | "dark";

const ThemeContext = createContext<{
  theme: Theme;
  toggleTheme: () => void;
}>({
  theme: "light",
  toggleTheme: () => {},
});

export const ThemeProvider = ({ children }: { children: React.ReactNode }) => {
  const [theme, setTheme] = useState<Theme>("light");

  useEffect(() => {
    const savedTheme = localStorage.getItem("theme") as Theme;
    if (savedTheme) setTheme(savedTheme);
  }, []);

  const toggleTheme = () => {
    const newTheme = theme === "light" ? "dark" : "light";
    setTheme(newTheme);
    localStorage.setItem("theme", newTheme);
  };

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      <div className={theme === "light" ? "theme-light" : "theme-dark"}>{children}</div>
    </ThemeContext.Provider>
  );
};

export const useTheme = () => useContext(ThemeContext);

```

* * *

## **Step 7: Testing and Debugging**

### Manual Testing

1. Toggle the theme and verify:
    - Background color changes.
    - Text and button colors adapt.
    - Saved preference persists after page reloads.

### Automated Testing

- Write unit tests for `ThemeProvider` and `ThemeToggle` using Jest and React Testing Library.

```tsx
import { render, screen } from "@testing-library/react";
import { ThemeProvider, useTheme } from "@/lib/theme";

test("toggles theme correctly", () => {
  const TestComponent = () => {
    const { theme, toggleTheme } = useTheme();
    return (
      <>
        <p data-testid="theme">{theme}</p>
        <button onClick={toggleTheme}>Toggle</button>
      </>
    );
  };

  render(
    <ThemeProvider>
      <TestComponent />
    </ThemeProvider>
  );

  expect(screen.getByTestId("theme")).toHaveTextContent("light");
  screen.getByText("Toggle").click();
  expect(screen.getByTestId("theme")).toHaveTextContent("dark");
});

```

* * *

## **Step 8: Deploy and Verify**

Deploy your app on **Vercel** and:

1. Test light/dark mode on different browsers and devices.
2. Verify that the theme persists across page reloads.