---
id: k0mqugjnekj1ap0kyv2mmsg
title: GlobalsCss
desc: ''
updated: 1744608204876
created: 1744608204876
---
Updated globals.css
Streamlines layering and variables.

Adds support for dark mode using .dark.

Simplifies class application using Tailwind 4 dynamic utilities.

```
@import "tailwindcss";

@layer base {
  :root {
    --background: 0 0% 100%;
    --foreground: 0 0% 3.9%;
    --primary: 0 0% 9%;
    --primary-foreground: 0 0% 98%;
    --radius: 0.5rem;
    /* Extend with other color tokens as needed */
  }

  .dark {
    --background: 0 0% 3.9%;
    --foreground: 0 0% 98%;
    --primary: 0 0% 98%;
    --primary-foreground: 0 0% 9%;
  }

  body {
    @apply bg-[hsl(var(--background))] text-[hsl(var(--foreground))];
  }

  * {
    @apply border-[hsl(var(--border,0_0%_89.8%))];
  }
}

@layer utilities {
  .text-balance {
    text-wrap: balance;
  }
}

```