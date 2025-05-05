---
id: hte9i078vygbc1fbfhv0j1i
title: Vercel
desc: ''
updated: 1742539713432
created: 1742539701917
---

**deploy_worker.json**  
```json
// File: vercel.json
{
  "version": 2,
  "builds": [
    { "src": "package.json", "use": "@vercel/next" }
  ],
  "routes": [
    { "src": "/api/(.*)", "dest": "/api/$1" }
  ]
}
