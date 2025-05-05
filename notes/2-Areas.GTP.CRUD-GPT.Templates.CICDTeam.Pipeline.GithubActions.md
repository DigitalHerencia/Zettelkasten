---
id: 6616egsisnkajbskgl9rfit
title: GithubActions
desc: ''
updated: 1742529157774
created: 1742529133084
---
```yml
name: CI Pipeline

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Use Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '16'
      - name: Install dependencies
        run: npm install
      - name: Lint code
        run: npm run lint
      - name: Run tests
        run: npm run test
      - name: Build project
        run: npm run build

```