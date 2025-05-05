---
id: pvbd187k80r90oq7xhkqo44
title: 1-Overview
desc: ''
updated: 1742523566579
created: 1742523378078
---
# CRUD-GPT

## 1. Overview

--- 
### Agents

This architecture leverages your modern tech stack (Next.js 15, React 19, TypeScript, MongoDB, Mongoose, Clerk, Tailwind CSS, ShadCN UI, etc.) and organizes the development process into multiple specialized GPT “agents.” 

These agents run inside the ChatGPT Desktop App with a manual input/output workflow. The system is divided into teams and work-groups that mirror your project’s folder structure (e.g. app/, components/, lib/, etc.) with each workgroup handling a discrete responsibility:

### Work Groups

Each workgroup consists of three specialized GPT roles:

- Prompter: Converts high-level user ideas or PRDs into structured, domain‑specific tasks.
- Worker: Generates code, configurations, or templates based on the structured prompt.
- QA Checker: Validates, troubleshoots, and iterates on the output to ensure quality and adherence to best practices.

These “agents” work in series so that the output of one (properly formatted) becomes the input to the next—ensuring a clear, deterministic pipeline from idea to deployable code.

