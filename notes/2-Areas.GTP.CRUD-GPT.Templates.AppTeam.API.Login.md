---
id: 0euc4mxxmxkn79a62kwg6mi
title: Login
desc: ''
updated: 1742528593706
created: 1742528573007
---
```ts
import { NextResponse } from "next/server";
import { verifyUserCredentials } from "../../../lib/auth";

export async function POST(request: Request) {
  const body = await request.json();
  const { email, password } = body;
  
  try {
    const user = await verifyUserCredentials(email, password);
    if (!user) {
      return NextResponse.json({ error: "Invalid credentials" }, { status: 401 });
    }
    // Create session token or similar logic here
    return NextResponse.json({ message: "Login successful", user });
  } catch (error) {
    return NextResponse.json({ error: "Server error" }, { status: 500 });
  }
}

```