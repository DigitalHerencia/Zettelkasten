---
id: 6e6thz8kzkp38m52umtybcx
title: Overview
desc: ''
updated: 1744671238796
created: 1744670749081
---

# Design System Overview

---

Let’s break this down into a modular design system blueprint using atomic design principles, component-level abstraction, and modern UX page taxonomies drawn from tools like Linear, Superhuman, Vercel, and DesignOps best practices.


---

## Table of Contents

* [Categories](1-Projects.viral-next-js-project.vercel.projects.CourtJester.Mulligan.Design.Page.Categories)
* [Build](1-Projects.viral-next-js-project.vercel.projects.CourtJester.Mulligan.Design.Page.Build)
* [Typography](1-Projects.viral-next-js-project.vercel.projects.CourtJester.Mulligan.Design.Page.Typography)
* [Palette](1-Projects.viral-next-js-project.vercel.projects.CourtJester.Mulligan.Design.Page.Palette)
* [Wireframes](1-Projects.viral-next-js-project.vercel.projects.CourtJester.Mulligan.Design.Page.Wireframes)

---

  ## TL;DR 

| Concept | Result | 
|---|---|  
| **Every page is** **categorized** | Into 6 modern UX taxonomies (Workstation, Views, etc.) |
| **Component layout is** **deterministic** | Padding, layout, spacing is predictable from category context |
| **Colors + text are** **tokenized**      | You know what every element looks like before coding |
| **Wireframes are** **documented**        | Each page has a spacing/layout blueprint to scale rapidly |


---

# Labeled Directory Tree

```
┣ 📂app
 ┃ ┣ 📂admin
 ┃ ┃ ┗ 📂dashboard
 ┃ ┃ ┃ ┣ 📂cases
 ┃ ┃ ┃ ┃ ┣ 📂[id]
 ┃ ┃ ┃ ┃ ┃ ┗ 📜page.tsx    (Object Sheets)
 ┃ ┃ ┃ ┃ ┗ 📜page.tsx      (Views)
 ┃ ┃ ┃ ┣ 📂motions
 ┃ ┃ ┃ ┃ ┣ 📂[id]
 ┃ ┃ ┃ ┃ ┃ ┗ 📜page.tsx    (Object Sheets)
 ┃ ┃ ┃ ┃ ┗ 📜page.tsx      (Views)
 ┃ ┃ ┃ ┣ 📂notifications
 ┃ ┃ ┃ ┃ ┗ 📜page.tsx      (Preferences & Status)
 ┃ ┃ ┃ ┣ 📂offenders
 ┃ ┃ ┃ ┃ ┣ 📂[id]
 ┃ ┃ ┃ ┃ ┃ ┗ 📜page.tsx    (Object Sheets)
 ┃ ┃ ┃ ┃ ┗ 📜page.tsx      (Views)
 ┃ ┃ ┃ ┣ 📂settings
 ┃ ┃ ┃ ┃ ┗ 📜page.tsx      (Preferences & Status)
 ┃ ┃ ┃ ┣ 📂tools
 ┃ ┃ ┃ ┃ ┣ 📂case-upload
 ┃ ┃ ┃ ┃ ┃ ┗ 📜page.tsx    (Action Modules)
 ┃ ┃ ┃ ┃ ┣ 📂database-reset
 ┃ ┃ ┃ ┃ ┃ ┗ 📜page.tsx    (Action Modules)
 ┃ ┃ ┃ ┃ ┣ 📂help
 ┃ ┃ ┃ ┃ ┃ ┗ 📜page.tsx    (Preferences & Status)
 ┃ ┃ ┃ ┃ ┣ 📂motions-editor
 ┃ ┃ ┃ ┃ ┃ ┗ 📜page.tsx    (Action Modules)
 ┃ ┃ ┃ ┃ ┣ 📂mugshot-upload
 ┃ ┃ ┃ ┃ ┃ ┗ 📜page.tsx    (Action Modules)
 ┃ ┃ ┃ ┃ ┣ 📂offender-profile
 ┃ ┃ ┃ ┃ ┃ ┗ 📜page.tsx    (Action Modules)
 ┃ ┃ ┃ ┃ ┣ 📜loading.tsx   (Shells)
 ┃ ┃ ┃ ┃ ┗ 📜page.tsx      (Action Modules)
 ┃ ┃ ┃ ┣ 📜layout.tsx      (Shells)
 ┃ ┃ ┃ ┣ 📜loading.tsx     (Shells)
 ┃ ┃ ┃ ┗ 📜page.tsx        (Workstation)
```

---

# Labeled Directory Tree 

```
app/
├── confirmation/
│   └── page.tsx  (Preferences & Status)
├── layout.tsx    (Shells)
├── offender/
│   └── dashboard/
│       └── [id]/
│           ├── cases/
│           │   ├── [caseId]/
│           │   │   ├── loading.tsx (Shells)
│           │   │   └── page.tsx    (Object Sheets)
│           │   ├── loading.tsx     (Shells)
│           │   └── page.tsx        (Views)
│           ├── court-dates/
│           │   └── page.tsx  (Views)
│           ├── layout.tsx    (Shells)
│           ├── loading.tsx   (Shells)
│           ├── motions/
│           │   ├── [motionId]/
│           │   │   └── page.tsx  (Object Sheets)
│           │   └── page.tsx      (Views)
│           ├── notifications/
│           │   └── page.tsx      (Preferences)
│           ├── page.tsx          (Workstation)
│           ├── profile/
│           │   ├── error.tsx     (Shells)
│           │   ├── loading.tsx   (Shells)
│           │   └── page.tsx      (Object Sheets)
│           └── settings/
│               └── page.tsx      (Preferences)
└── page.tsx                      (Workstation)

```