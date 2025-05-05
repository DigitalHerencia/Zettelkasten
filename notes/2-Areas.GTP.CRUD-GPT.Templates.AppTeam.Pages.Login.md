---
id: ip5d85gajo712z7p6hpy8so
title: Login
desc: ''
updated: 1742528332331
created: 1742528308610
---
```tsx
"use client";
import React, { useState } from "react";
import Button from "../../components/Button";

const LoginPage = () => {
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");
  const [loading, setLoading] = useState(false);

  const handleSubmit = async (e: React.FormEvent) => {
    e.preventDefault();
    setLoading(true);
    // Call API endpoint /api/login
    // Handle API response and error handling here
    setLoading(false);
  };

  return (
    <div className="container mx-auto p-4">
      <h1 className="text-2xl font-bold mb-4">Login</h1>
      <form onSubmit={handleSubmit} className="space-y-4">
        <input
          type="email"
          placeholder="Email"
          value={email}
          onChange={(e) => setEmail(e.target.value)}
          className="border p-2 w-full"
        />
        <input
          type="password"
          placeholder="Password"
          value={password}
          onChange={(e) => setPassword(e.target.value)}
          className="border p-2 w-full"
        />
        <Button type="submit" disabled={loading}>
          {loading ? "Logging in..." : "Login"}
        </Button>
      </form>
      <div className="mt-4">
        <a href="/forgot-password" className="text-blue-600">
          Forgot Password?
        </a>
        <span> | </span>
        <a href="/signup" className="text-blue-600">
          Sign Up
        </a>
      </div>
    </div>
  );
};

export default LoginPage;

```