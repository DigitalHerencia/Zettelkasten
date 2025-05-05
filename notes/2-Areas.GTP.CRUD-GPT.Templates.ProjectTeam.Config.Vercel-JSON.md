---
id: nzd8swkf0hvsxgfwcr7znzo
title: Vercel-JSON
desc: ''
updated: 1742526328783
created: 1742526202269
---
{
  "version": 2,
  "builds": [
    { "src": "package.json", "use": "@vercel/next" }
  ],
  "routes": [
    { "src": "/api/(.*)", "dest": "/api/$1" }
  ]
}
