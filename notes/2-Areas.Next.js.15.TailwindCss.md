---
id: qcaoonssgmiq1hrnundcbjo
title: TailwindCss
desc: ''
updated: 1744608243734
created: 1744608243734
---
Updated tailwind.config.ts
Removes legacy theme.extend for color tokens (you now define these in CSS).

Uses Tailwind 4 CSS-first architecture.

Keeps necessary plugin (tailwindcss-animate).

```ts
import { defineConfig } from "tailwindcss"

export default defineConfig({
  darkMode: "class", // uses .dark selector
  content: [], // Tailwind v4 detects files automatically
  plugins: [require("tailwindcss-animate")],
})

```