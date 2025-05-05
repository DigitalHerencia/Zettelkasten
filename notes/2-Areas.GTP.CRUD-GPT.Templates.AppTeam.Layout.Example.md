---
id: 23lkqbzenycyi47f44uehp9
title: Example
desc: ''
updated: 1742537621628
created: 1742537613407
---

**layout_worker.tsx**  
```tsx
// File: app/layout.tsx
import React from "react";
import Header from "../components/Header";
import Sidebar from "../components/Sidebar";
import Footer from "../components/Footer";

const MainLayout: React.FC<{ children: React.ReactNode }> = ({ children }) => {
  return (
    <div className="min-h-screen flex flex-col">
      <Header />
      <div className="flex flex-1">
        <Sidebar />
        <main className="flex-1 p-4">{children}</main>
      </div>
      <Footer />
    </div>
  );
};

export default MainLayout;
