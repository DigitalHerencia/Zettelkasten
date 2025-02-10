---
id: za17xvf3ndi2pu5cqr7am4p
title: redux-toolkit
desc: ''
updated: 1733340369073
created: 1733340180418
---

### Lesson 6: **State Management with Redux Toolkit**

*(Manage complex application state effectively and efficiently.)*

* * *

#### What is Redux Toolkit?

- **Definition**: A modern, opinionated way to use Redux, a predictable state container for JavaScript apps.
- **Why Redux Toolkit?**
    - Simplifies the setup process.
    - Reduces boilerplate code.
    - Comes with tools like `createSlice` and `createAsyncThunk` for easier development.

* * *

#### When Do You Need Redux?

- Use Redux if your app:
    - Shares state across multiple components/pages.
    - Manages complex state (e.g., authentication, data fetching).
    - Requires debugging tools like **Redux DevTools**.

* * *

#### Core Concepts of Redux Toolkit

| Concept | Description |
| --- | --- |
| **Store** | Central place where your app’s state lives. |
| **Slice** | A collection of reducers and actions related to a specific feature. |
| **Reducer** | A pure function that updates the state based on an action. |
| **Action** | A plain JavaScript object that describes what happened (e.g., `ADD_TODO`). |
| **Dispatch** | Sends an action to the store to update the state. |
| **Selector** | A function to retrieve a specific piece of state from the store. |

* * *

#### Installing Redux Toolkit in a Next.js Project

1. **Install Redux Toolkit and React Redux**:

    - Run:

            bashCopy codenpm install @reduxjs/toolkit react-redux
2. **Setup the Redux Store**:

    - Create a new folder `store/` in your project root.
    - Add a file `store/index.js`:

            javascriptCopy codeimport { configureStore } from '@reduxjs/toolkit';import counterReducer from './counterSlice'; export const store = configureStore({ reducer: { counter: counterReducer, },});

* * *

#### Example: Counter Slice

1. **Create the Counter Slice**:

    - Add a file `store/counterSlice.js`:

            javascriptCopy codeimport { createSlice } from '@reduxjs/toolkit'; const counterSlice = createSlice({ name: 'counter', initialState: { value: 0 }, reducers: { increment: (state) => { state.value += 1; }, decrement: (state) => { state.value -= 1; }, incrementByAmount: (state, action) => { state.value += action.payload; }, },}); export const { increment, decrement, incrementByAmount } = counterSlice.actions;export default counterSlice.reducer;
2. **Provide the Store to Your App**:

    - Wrap your app with the `Provider` in `_app.js`:

            javascriptCopy codeimport { Provider } from 'react-redux';import { store } from '@/store'; export default function App({ Component, pageProps }) { return ( <Provider store={store}> <Component {...pageProps} /> </Provider> );}

* * *

#### Using Redux in a Component

1. **Update `pages/index.js`**:
    - Example counter functionality:

            javascriptCopy codeimport { useSelector, useDispatch } from 'react-redux';import { increment, decrement, incrementByAmount } from '@/store/counterSlice'; export default function Home() { const count = useSelector((state) => state.counter.value); const dispatch = useDispatch(); return ( <div className="flex flex-col items-center justify-center min-h-screen bg-gray-100"> <h1 className="text-3xl font-bold">Counter: {count}</h1> <div className="mt-4 space-x-4"> <button className="px-4 py-2 text-white bg-blue-500 rounded hover:bg-blue-600" onClick={() => dispatch(increment())} > Increment </button> <button className="px-4 py-2 text-white bg-red-500 rounded hover:bg-red-600" onClick={() => dispatch(decrement())} > Decrement </button> <button className="px-4 py-2 text-white bg-green-500 rounded hover:bg-green-600" onClick={() => dispatch(incrementByAmount(5))} > Increment by 5 </button> </div> </div> );}

* * *

#### Understanding Redux Flow

**Diagram**:

    plaintextCopy code[ Component ] ---> dispatch(action) ---> [ Reducer ] ---> update state in [ Store ] ---> re-render Component

* * *

#### Challenge: Build a Todo List

1. **Requirements**:
    - A `todoSlice` to manage an array of todos (add, remove, toggle complete).
    - A component with:
        - An input field to add new todos.
        - A list of todos displayed with a delete button.
    - Use Redux selectors and dispatch to manage state.

* * *

#### Resources:

- Redux Toolkit Docs
- Learn Redux with Practical Examples