---
id: r5uswfbmvzwxudy8c2kefh3
title: Button
desc: ''
updated: 1742538553538
created: 1742538173158
---

**component_worker.tsx**  
```tsx
// File: components/Button.tsx
import React from "react";

interface ButtonProps extends React.ButtonHTMLAttributes<HTMLButtonElement> {
  children: React.ReactNode;
}

const Button: React.FC<ButtonProps> = ({ children, className, ...props }) => {![[Prompter|2-Areas.GTP.CRUD-GPT.CustomInstructions.AppTeam.API.Prompter]]
    <button
      {...props}
      className={`px-4 py-2 rounded bg-blue-600 text-white hover:bg-blue-700 ${className || ""}`}
    >
      {children}
    </button>
  );
};

export default Button;
