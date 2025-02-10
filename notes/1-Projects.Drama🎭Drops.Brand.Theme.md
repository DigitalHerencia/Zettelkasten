---
id: ehtppizdvz4iuq4l38hlu75
title: Theme
desc: ''
updated: 1736657829505
created: 1736657483494
---

# **Theme for Drama🎭Drops Pages**
___

Here's a tailored solution that includes a custom tailwind.config.js and a global CSS file (globals.css) for your Next.js project using the specified colors and Fira Mono font. The implementation also incorporates Tailwind variables to create a ShadCN-like theme system.

## 1. Tailwind Configuration (tailwind.config.js)

```javascript
const { fontFamily } = require('tailwindcss/defaultTheme');

/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    './pages/**/*.{js,ts,jsx,tsx}',
    './components/**/*.{js,ts,jsx,tsx}',
    './app/**/*.{js,ts,jsx,tsx}',
  ],
  theme: {
    extend: {
      colors: {
        white: '#ffffff',
        black: '#000000',
        primary: '#730437',
        secondary: '#e9b44f',
      },
      fontFamily: {
        mono: ['Fira Mono', ...fontFamily.mono],
      },
    },
  },
  plugins: [],
};

```

## 2. Global CSS (globals.css)

This file uses CSS variables for theming and integrates the Tailwind configuration.

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

:root {
  --color-white: theme(colors.white);
  --color-black: theme(colors.black);
  --color-primary: theme(colors.primary);
  --color-secondary: theme(colors.secondary);
  --font-mono: theme(fontFamily.mono);
}

body {
  @apply bg-white text-black font-mono;
}

/* Custom ShadCN-inspired styles */
.theme-light {
  --color-bg: var(--color-white);
  --color-text: var(--color-black);
}

.theme-dark {
  --color-bg: var(--color-black);
  --color-text: var(--color-white);
}

[data-theme='primary'] {
  --color-accent: var(--color-primary);
  --color-accent-contrast: var(--color-secondary);
}

[data-theme='secondary'] {
  --color-accent: var(--color-secondary);
  --color-accent-contrast: var(--color-primary);
}

.button {
  @apply px-4 py-2 rounded transition;
  background-color: var(--color-accent);
  color: var(--color-accent-contrast);
}

.button:hover {
  filter: brightness(1.1);
}

.card {
  @apply p-4 border rounded-lg;
  background-color: var(--color-bg);
  color: var(--color-text);
}

```


## 3. Using in a Next.js Project

Install Dependencies:

- Install the required font and Tailwind CSS:

```bash
npm install tailwindcss postcss autoprefixer
npm install @fontsource/fira-mono

```

- Include Font in _app.js:

```javascript
import '@fontsource/fira-mono';
import '../styles/globals.css';

```

Enable Theming in Layout or Components: 

- Add a wrapper around your application to toggle themes using data-theme attributes:

```jsx
import { useState } from 'react';

export default function MyApp({ Component, pageProps }) {
  const [theme, setTheme] = useState('primary');

  return (
    <div data-theme={theme}>
      <button onClick={() => setTheme(theme === 'primary' ? 'secondary' : 'primary')}>
        Toggle Theme
      </button>
      <Component {...pageProps} />
    </div>
  );
}

```
