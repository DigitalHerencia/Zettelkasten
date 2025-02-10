---
id: wj6nu1xnqjt0vsi8d5ozi2o
title: debugging-and-troubleshooting
desc: ''
updated: 1733341981618
created: 1733341953605
---

### Lesson 24: **Linting and Formatting with ESLint and Prettier**

*(Keep your code clean, consistent, and error-free.)*

* * *

#### What is ESLint?

- **Definition**: A tool to find and fix problems in JavaScript/TypeScript code.
- **Purpose**: Ensures code quality and consistency by enforcing rules.

#### What is Prettier?

- **Definition**: An opinionated code formatter that ensures consistent styling.
- **Purpose**: Automatically formats code to a specified style.

* * *

### Step 1: Install and Configure ESLint

1. **Install ESLint**:

        bashCopy codenpm install eslint --save-dev
2. **Initialize ESLint**:

        bashCopy codenpx eslint --init

    - Choose:
        - **How to use?** JavaScript or TypeScript with React.
        - **Format?** JSON or JavaScript for configuration.
3. **Create an ESLint Config File**:

    - Example `.eslintrc.json`:

            jsonCopy code{ "env": { "browser": true, "es2021": true }, "extends": ["eslint:recommended", "plugin:react/recommended"], "parserOptions": { "ecmaVersion": 12, "sourceType": "module" }, "rules": { "no-unused-vars": "warn", "react/prop-types": "off" }}
4. **Run ESLint**:

        bashCopy codenpx eslint . --fix

    - Lints and fixes errors in your codebase.

* * *

### Step 2: Install and Configure Prettier

1. **Install Prettier**:

        bashCopy codenpm install --save-dev prettier
2. **Create a Prettier Config File**:

    - Add `.prettierrc`:

            jsonCopy code{ "semi": true, "singleQuote": true, "tabWidth": 2}
3. **Format Your Code**:

        bashCopy codenpx prettier --write .

* * *

### Step 3: Integrate ESLint and Prettier

1. **Install Plugins**:

        bashCopy codenpm install --save-dev eslint-config-prettier eslint-plugin-prettier
2. **Update `.eslintrc.json`**:

        jsonCopy code{ "extends": ["eslint:recommended", "plugin:react/recommended", "prettier"], "plugins": ["prettier"], "rules": { "prettier/prettier": "error" }}
3. **Run ESLint and Prettier Together**:

        bashCopy codenpx eslint . --fix