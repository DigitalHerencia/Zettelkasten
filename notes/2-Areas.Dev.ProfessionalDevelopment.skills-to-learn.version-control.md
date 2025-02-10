---
id: 65x1etbjty44vl0xrcpr5uv
title: version-control
desc: ''
updated: 1733341803022
created: 1733341777938
---

### Lesson 23: **Version Control with Git and GitHub**

*(Learn how to manage your codebase, collaborate, and track changes effectively.)*

* * *

#### What is Version Control?

- **Definition**: A system that records changes to a file or set of files over time, enabling you to revert, share, and manage code collaboratively.
- **Key Tool**: Git is the most widely used version control system, often paired with GitHub for remote repositories.

* * *

#### Why Use Git and GitHub?

| Feature | Benefit |
| --- | --- |
| **Collaboration** | Allows multiple developers to work on the same project. |
| **Change Tracking** | Tracks every change made to the codebase. |
| **Branching** | Enables working on features or fixes without disrupting the main code. |
| **Backup** | Provides a cloud-based backup of your project. |

* * *

### Step 1: Initialize a Git Repository

1. **Initialize Git**:

        bashCopy codegit init

    - Creates a `.git` folder to track your project.
2. **Check Git Status**:

        bashCopy codegit status

    - Shows the current state of your repository.
3. **Add Files**:

        bashCopy codegit add .

    - Stages all files for the next commit.
4. **Commit Changes**:

        bashCopy codegit commit -m "Initial commit"

    - Saves a snapshot of the current state of your project.

* * *

### Step 2: Push to GitHub

1. **Create a New Repository on GitHub**:

    - Go to [GitHub](https://github.com/) and create a new repository.
2. **Add the Remote Origin**:

        bashCopy codegit remote add origin https://github.com/your-username/repo-name.git
3. **Push Your Code**:

        bashCopy codegit branch -M maingit push -u origin main

* * *

### Step 3: Branching and Merging

1. **Create a New Branch**:

        bashCopy codegit checkout -b feature/new-feature
2. **Merge the Branch**:

    - Switch back to `main`:

            bashCopy codegit checkout main
    - Merge changes:

            bashCopy codegit merge feature/new-feature
3. **Resolve Conflicts**:

    - Git will prompt you to resolve any conflicts manually.

* * *

### Step 4: Collaborate with Pull Requests

1. **Push the Feature Branch**:

        bashCopy codegit push -u origin feature/new-feature
2. **Create a Pull Request on GitHub**:

    - Go to your repository → Pull Requests → New Pull Request.
3. **Review and Merge**:

    - Team members can review the code and merge it into the `main` branch.