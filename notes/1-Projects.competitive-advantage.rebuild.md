---
id: v2mrfz0assbwqvlsw8bdr6s
title: rebuild
desc: ''
updated: 1727235573648
created: 1727119779460
---

<div style="display: flex; justify-content: center; align-items: center;">

<img src="https://files.oaiusercontent.com/file-01FWQuUMRfNUDGJj5CPMwOUC?se=2124-04-14T00%3A49%3A50Z&sp=r&sv=2023-11-03&sr=b&rscc=max-age%3D1209600%2C%20immutable&rscd=attachment%3B%20filename%3Dlogo512.png&sig=XZy3I1Py7MUzqJVr8XbLvI0tFm3B2/Vcy93Dk3YvmCU%3D" width="58"/>

&nbsp;&nbsp;&nbsp;&nbsp;

# MERN Full Stack Web App

</div>

## **Project Synopsis: New Mexico Cannabis Retail Analytics**

### Overview

The **New Mexico Cannabis Retail Analytics** project is a major rebuild and optimization of an existing MERN stack application focused on retail analytics for the cannabis industry. The goal is to enhance performance, scalability, and maintainability by migrating to more modern technologies and architectures.

### Key Changes:

-   **Frontend Migration to Next.js**: Moving from React to **Next.js** for better SEO, performance, and server-side rendering (SSR). Next.js allows for faster initial page loads, dynamic page generation, and improved overall user experience.
-   **Backend Refactor to NestJS**: The backend is being refactored to **NestJS**, a modular and scalable Node.js framework. This change will improve code organization, maintainability, and enable the use of TypeScript for better type safety and clearer architecture.
-   **State Management Optimization with Recoil**: **Redux** is being replaced with **Recoil**, which offers a simpler API for state management. Recoil allows for better control over local and global state, reducing the complexity of managing application state and improving responsiveness.
-   **Redis Integration**: Adding **Redis** for caching frequently accessed data (such as sales trends and product details) will reduce load on the MongoDB database and speed up API responses.
-   **MongoDB Optimizations**: Using MongoDB **aggregation pipelines** and **indexing** for faster queries and data retrieval, particularly for complex reports such as sales trends and product comparisons.
-   **Serverless Deployment**: The app will be deployed using **serverless architectures** like **Vercel** for the frontend and **AWS Lambda** for the backend. This will reduce infrastructure management overhead, ensure auto-scaling, and lower operational costs.

___

## **Project Strategy**

The primary strategy for rebuilding this application is to adopt **modern frameworks** and **best practices** that will ensure the app remains efficient, scalable, and easy to maintain over time. The migration to **Next.js** and **NestJS**, along with the shift to **serverless architecture**, will enable the application to handle higher traffic while maintaining optimal performance.

-   **Next.js** provides server-side rendering and static site generation, significantly improving page load times and SEO performance for cannabis retailers looking to reach a broader customer base.
-   **NestJS** introduces a modular architecture, making it easier to scale individual services like user management, product catalog, and sales analytics as needed.
-   **Recoil** reduces boilerplate and complexity compared to Redux, improving state management efficiency, especially in highly interactive pages.
-   **Redis** will be leveraged for caching to minimize database load and improve performance on key features like product comparison and market share visualization.
-   **MongoDB Atlas** will be utilized for automated backups, scaling, and performance monitoring.

___

## **Links**

### 1\. [[Summary|dendron://PARA-Militant-MIND(x2)_v02-001_07-28-2024 /1-Projects.competitive-advantage.rebuild.summary]]
    
 A concise summary of the overall project, including key changes and the rationale behind the migration to newer technologies.

### 2\. [[Plan|dendron://PARA-Militant-MIND(x2)_v02-001_07-28-2024 /1-Projects.competitive-advantage.rebuild.plan]]
    
 The comprehensive plan for rebuilding the application, including timelines, checklists, and steps to integrate modern frameworks, optimize performance, and ensure scalability.
    
### 3\.  [[Tech-Stack|dendron://PARA-Militant-MIND(x2)_v02-001_07-28-2024 /1-Projects.competitive-advantage.rebuild.summary.tech-stack]]
    
An in-depth description of the current and proposed technology stack, detailing the shift from MERN to the more modern Next.js, NestJS, Recoil, and serverless deployment.

### 4\. [[Directory-Tree|dendron://PARA-Militant-MIND(x2)_v02-001_07-28-2024 /1-Projects.competitive-advantage.rebuild.plan.directory-tree]]
    
 A detailed breakdown of the proposed directory structure for the rebuilt application, including Next.js and NestJS modules, state management with Recoil, and integrations like Redis.