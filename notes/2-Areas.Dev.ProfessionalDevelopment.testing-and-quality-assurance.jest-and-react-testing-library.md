---
id: qgjsbyqaph48ppaa80idxg7
title: jest-and-react-testing-library
desc: ''
updated: 1733341252405
created: 1733341200564
---

### Lesson 18: **Unit Testing with Jest and React Testing Library**

*(Ensure the reliability of your components and logic with effective testing.)*

* * *

#### What is Unit Testing?

- **Definition**: Testing individual components or functions to ensure they work as expected in isolation.
- **Key Tools**:
    - **Jest**: A JavaScript testing framework for unit and integration testing.
    - **React Testing Library (RTL)**: A library for testing React components with a focus on user interactions.

* * *

#### Why Use Jest and RTL?

| Feature | Benefit |
| --- | --- |
| **Fast** | Optimized for performance with minimal setup. |
| **Intuitive APIs** | Simple and declarative testing syntax. |
| **Component Testing** | Ensures UI components behave as intended. |
| **Mocks and Spies** | Simulate functions and dependencies. |

* * *

### Step 1: Set Up Jest and RTL

1. **Install Jest and React Testing Library**:

        bashCopy codenpm install --save-dev jest @testing-library/react @testing-library/jest-dom
2. **Configure Jest**:

    - Add the following to `package.json`:

            jsonCopy code"jest": { "testEnvironment": "jsdom"}
    - Or create a `jest.config.js` file:

            javascriptCopy codemodule.exports = { testEnvironment: 'jsdom', setupFilesAfterEnv: ['@testing-library/jest-dom'],};
3. **Add a Test Script**:

    - Update `package.json`:

            jsonCopy code"scripts": { "test": "jest"}

* * *

### Step 2: Write Your First Test

1. **Create a Component**:

    - Add a file `components/Button.js`:

            javascriptCopy codeexport default function Button({ label, onClick }) { return ( <button onClick={onClick} className="px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600" > {label} </button> );}
2. **Write a Test**:

    - Create a file `components/Button.test.js`:

            javascriptCopy codeimport { render, screen, fireEvent } from '@testing-library/react';import Button from './Button'; test('renders button with label', () => { render(<Button label="Click Me" />); const button = screen.getByText('Click Me'); expect(button).toBeInTheDocument();}); test('calls onClick when clicked', () => { const handleClick = jest.fn(); render(<Button label="Click Me" onClick={handleClick} />); const button = screen.getByText('Click Me'); fireEvent.click(button); expect(handleClick).toHaveBeenCalledTimes(1);});
3. **Run the Test**:

    - Run the test command:

            bashCopy codenpm test

* * *

### Step 3: Testing a React Component with State

1. **Create a Counter Component**:

    - Add a file `components/Counter.js`:

            javascriptCopy codeimport { useState } from 'react'; export default function Counter() { const [count, setCount] = useState(0); return ( <div className="text-center"> <h1 data-testid="count">{count}</h1> <button onClick={() => setCount(count + 1)} className="px-4 py-2 bg-green-500 text-white rounded hover:bg-green-600" > Increment </button> </div> );}
2. **Write a Test for the Counter**:

    - Add a file `components/Counter.test.js`:

            javascriptCopy codeimport { render, screen, fireEvent } from '@testing-library/react';import Counter from './Counter'; test('renders initial count', () => { render(<Counter />); const count = screen.getByTestId('count'); expect(count).toHaveTextContent('0');}); test('increments count when button is clicked', () => { render(<Counter />); const button = screen.getByText('Increment'); const count = screen.getByTestId('count'); fireEvent.click(button); expect(count).toHaveTextContent('1');});

* * *

### Testing Best Practices

| Principle | Explanation |
| --- | --- |
| **Test User Behavior** | Focus on what the user experiences, not implementation. |
| **Keep Tests Small** | Test one thing at a time for clarity. |
| **Mock External Dependencies** | Simulate APIs, database calls, etc., for isolated tests. |

* * *

### Step 4: Mocking API Calls

1. **Mock a Fetch Request**:

    - Add a file `components/UserList.js`:

            javascriptCopy codeimport { useEffect, useState } from 'react'; export default function UserList() { const [users, setUsers] = useState([]); useEffect(() => { fetch('https://jsonplaceholder.typicode.com/users') .then((res) => res.json()) .then((data) => setUsers(data)); }, []); return ( <ul> {users.map((user) => ( <li key={user.id}>{user.name}</li> ))} </ul> );}
2. **Write a Test with a Mock**:

    - Add a file `components/UserList.test.js`:

            javascriptCopy codeimport { render, screen } from '@testing-library/react';import UserList from './UserList'; global.fetch = jest.fn(() => Promise.resolve({ json: () => Promise.resolve([{ id: 1, name: 'John Doe' }, { id: 2, name: 'Jane Smith' }]), })); test('renders user list', async () => { render(<UserList />); const users = await screen.findAllByRole('listitem'); expect(users).toHaveLength(2); expect(users[0]).toHaveTextContent('John Doe');});

* * *

### Practice Task

1. **Challenge**: Write tests for a `TodoList`component that:
    - Displays a list of todos.
    - Adds a new todo when a form is submitted.
2. **Bonus**: Mock an API call to fetch todos dynamically.

### Advanced Features

1. **Snapshots**:

    - Use Jest snapshots to ensure UI components don’t unintentionally change.

            javascriptCopy codeimport { render } from '@testing-library/react';import Button from './Button'; test('matches snapshot', () => { const { asFragment } = render(<Button label="Snapshot Button" />); expect(asFragment()).toMatchSnapshot();});
2. **Integration with CI/CD**:

    - Add tests to your GitHub Actions or other CI pipelines for automated testing.

* * *

### Resources

- Jest Documentation
- React Testing Library
- Learn interactively: [Jest & RTL Crash Course](https://www.youtube.com/watch?v=9mD1B7Sfts8)