---
id: s4bcxtq51mimjjv27eie2jp
title: react-19
desc: ''
updated: 1733338948306
created: 1733338587422
---

# Lesson 1: **Frameworks & Libraries - React Basics**

*(Building the foundation for modern frontend development.)*

**Objective:** Understand React, its purpose, and create a simple "Hello World" React app.

* * *

## What is React?

- **Definition**: A JavaScript library for building user interfaces, particularly Single Page Applications (SPAs).
- **Why Use React?**
    - Component-based architecture (reusable UI pieces).
    - Virtual DOM for efficient rendering.
    - Easy integration with other libraries and frameworks.

* * *

## Key Concepts in React:

| Concept | Description |
| --- | --- |
| **Component** | A reusable piece of UI. Example: A button or a form. |
| **JSX** | A syntax extension that looks like HTML but works in JavaScript. |
| **Props** | Input data passed to a component (short for properties). |
| **State** | A component's internal data that can change over time. |
| **Hooks** | Functions like `useState` or `useEffect` for managing state and side effects. |

* * *

## Interactive Activity: Create Your First React App

1. **Setup**:

    - Install Node.js from [Node.js official website](https://nodejs.org).
    - Use the terminal to run:

            bashCopy codenpx create-react-app my-first-react-appcd my-first-react-appnpm start
    - This will start a development server and open a browser tab with a React app.
2. **Code Exercise**:

    - Open `src/App.js` and replace its content with:

            jsxCopy codefunction App() { const name = "React Learner"; return ( <div> <h1>Hello, {name}!</h1> <p>Welcome to your first React app.</p> </div> );}export default App;
    - Save the file. Observe how the browser reloads automatically to reflect your changes.

* * *

## Diagram: React App Structure

    plaintextCopy codesrc/├── App.js <-- Main component├── index.js <-- Entry point├── components/ <-- (Future custom components will go here)

* * *

## Practice:

1. **Task**: Add a new `<button>` below the paragraph that says "Click me!" and log a message to the console when clicked.
2. **Hint**: Use an `onClick` event handler.

* * *

## Resources:

- Official React Documentation
- Free interactive course: React Basics on Scrimba