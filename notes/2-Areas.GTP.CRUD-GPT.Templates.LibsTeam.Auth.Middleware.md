---
id: hku5z7tcer9fphf8tr7ld7m
title: Middleware
desc: ''
updated: 1742539971691
created: 1742539958581
---

**auth_worker.ts**  
```ts
// File: lib/auth/authMiddleware.ts
import { NextRequest, NextResponse } from "next/server";
import jwt from "jsonwebtoken";
import { getUserByEmail } from "./userService"; // hypothetical service

export async function authMiddleware(request: NextRequest) {
  const token = request.headers.get("authorization")?.split(" ")[1];
  if (!token) {
    return NextResponse.json({ error: "Unauthorized" }, { status: 401 });
  }
  try {
    const decoded = jwt.verify(token, process.env.JWT_SECRET!);
    // Attach user to request or validate permissions here
    return NextResponse.next();
  } catch (error) {
    return NextResponse.json({ error: "Invalid token" }, { status: 403 });
  }
}


