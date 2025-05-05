---
id: 7zfaqai64e8ffb30lf204se
title: Index
desc: ''
updated: 1742528941078
created: 1742528928552
---
```ts
export interface ApiResponse<T> {
  data?: T;
  error?: string;
}

export interface User {
  id: string;
  email: string;
  role: "user" | "mod" | "admin" | "dev";
}

```