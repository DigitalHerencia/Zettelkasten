---
id: 224vwxmlypp24lcpsgbm70e
title: Use
desc: ''
updated: 1742528746981
created: 1742528734970
---
```ts
import mongoose, { Schema, Document } from "mongoose";

export interface IUser extends Document {
  email: string;
  passwordHash: string;
  role: "user" | "mod" | "admin" | "dev";
  createdAt: Date;
  updatedAt: Date;
}

const UserSchema: Schema = new Schema(
  {
    email: { type: String, required: true, unique: true },
    passwordHash: { type: String, required: true },
    role: { type: String, enum: ["user", "mod", "admin", "dev"], default: "user" }
  },
  { timestamps: true }
);

export default mongoose.models.User || mongoose.model<IUser>("User", UserSchema);
```