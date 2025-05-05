---
id: 6zpgs02fjaekukaeqf5pzcn
title: Helpers
desc: ''
updated: 1742539958776
created: 1742528817550
---
```ts
export const formatDate = (date: Date): string => {
  return date.toLocaleDateString("en-US", {
    year: "numeric",
    month: "long",
    day: "numeric"
  });![[Middleware|2-Areas.GTP.CRUD-GPT.Templates.LibsTeam.Auth.Middleware]]

export const currencyFormatter = (value: number): string => {
  return new Intl.NumberFormat("en-US", { style: "currency", currency: "USD" }).format(value);
};

```