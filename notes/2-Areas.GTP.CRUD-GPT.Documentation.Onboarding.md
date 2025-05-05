---
id: deg1dg58s24ulebreg149ku
title: Onboarding
desc: ''
updated: 1742530293763
created: 1742530244879
---
### **How to Onboard a New Team Member**

1. **Understand the Flow:** The AI system is structured like a **real development team** with:

    - **Prompters** that take high-level input and generate structured tasks.
    - **Workers** that generate actual code.
    - **QA Agents** that validate and troubleshoot outputs.
2. **Know the AI Agents:** Each workgroup has **three GPTs (Prompter, Worker, QA)**.

    - If you need **a UI page**, start with the **Frontend Prompter**.
    - If you need **a database model**, use the **Model Prompter**.
    - If you need **to deploy**, use the **Deployment GPTs**.
3. **Follow the Workflow:**

    - **Feed the Prompter GPT** with feature requests → Get structured tasks.
    - **Send structured tasks to Worker GPT** → Get code output.
    - **Run the code through QA GPT** → Get error checking & validation.
    - **Copy/paste the validated output into the project**.
4. **Check the Project Files:**

    - Read through `README.md` and `docs/` for project structure.
    - Review `ci/github-actions.yml` for deployment workflows.
    - Familiarize yourself with the **Next.js file structure** in `/app`, `/components`, `/lib`.
5. **Tools You’ll Be Using:**

    - **ChatGPT Desktop App** → To interact with the AI agents.
    - **VS Code** → To write and integrate generated code.
    - **GitHub** → For version control.
    - **Vercel** → For hosting and deployments.

* * *
