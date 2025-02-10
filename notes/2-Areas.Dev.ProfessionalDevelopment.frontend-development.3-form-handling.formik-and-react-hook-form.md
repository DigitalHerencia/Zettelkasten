---
id: fbrjoyhu5o5r3p1xhwd35ey
title: formik-and-react-hook-form
desc: ''
updated: 1733340369063
created: 1733340334179
---

### Lesson 8: **Form Handling with Formik and React Hook Form**

*(Efficiently handle user input and validation in your apps.)*

* * *

#### Why Use Form Libraries?

Forms are essential in web applications, but handling form state, validation, and submission can be complex. Formik and React Hook Form simplify this process by providing tools to:

- Manage form state.
- Perform validation.
- Handle errors and submissions.

* * *

### **Formik**

- **Definition**: A form library for React that simplifies form state management and validation.
- **Why Use Formik?**
    - Declarative and easy to use.
    - Built-in integration with popular validation libraries like Yup.

* * *

#### Installing Formik

1. Install Formik and Yup:

        bashCopy codenpm install formik yup

* * *

#### Example: Basic Login Form with Formik

1. **Code Example**:

    - Create a new file `pages/login.js`:

            javascriptCopy codeimport { Formik, Form, Field, ErrorMessage } from 'formik';import * as Yup from 'yup'; const LoginSchema = Yup.object().shape({ email: Yup.string().email('Invalid email').required('Required'), password: Yup.string().min(6, 'Too short!').required('Required'),}); export default function Login() { return ( <div className="min-h-screen flex items-center justify-center bg-gray-100"> <Formik initialValues={{ email: '', password: '' }} validationSchema={LoginSchema} onSubmit={(values) => { console.log(values); }} > {() => ( <Form className="space-y-4"> <div> <label>Email:</label> <Field name="email" type="email" className="block border rounded px-2 py-1" /> <ErrorMessage name="email" component="div" className="text-red-500" /> </div> <div> <label>Password:</label> <Field name="password" type="password" className="block border rounded px-2 py-1" /> <ErrorMessage name="password" component="div" className="text-red-500" /> </div> <button type="submit" className="px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600" > Login </button> </Form> )} </Formik> </div> );}
2. **Explanation**:

    - `Formik`: Provides the form state and handlers.
    - `Field`: Manages the input field.
    - `ErrorMessage`: Displays validation errors.
    - `Yup`: Defines a validation schema.

* * *

#### Advantages of Formik

| Feature | Benefit |
| --- | --- |
| **Integration with Yup** | Simplifies form validation. |
| **Declarative Syntax** | Easy to read and write. |
| **Controlled Inputs** | Automatic handling of form state and values. |

* * *

### **React Hook Form (RHF)**

- **Definition**: A lightweight library for managing form state with minimal re-renders.
- **Why Use React Hook Form?**
    - Uncontrolled inputs for better performance.
    - Built-in validation.
    - Simple API for complex forms.

* * *

#### Installing React Hook Form

1. Install React Hook Form:

        bashCopy codenpm install react-hook-form

* * *

#### Example: Basic Signup Form with React Hook Form

1. **Code Example**:

    - Create a new file `pages/signup.js`:

            javascriptCopy codeimport { useForm } from 'react-hook-form'; export default function Signup() { const { register, handleSubmit, formState: { errors }, } = useForm(); const onSubmit = (data) => { console.log(data); }; return ( <div className="min-h-screen flex items-center justify-center bg-gray-100"> <form onSubmit={handleSubmit(onSubmit)} className="space-y-4"> <div> <label>Email:</label> <input {...register('email', { required: 'Email is required' })} type="email" className="block border rounded px-2 py-1" /> {errors.email && <p className="text-red-500">{errors.email.message}</p>} </div> <div> <label>Password:</label> <input {...register('password', { required: 'Password is required' })} type="password" className="block border rounded px-2 py-1" /> {errors.password && <p className="text-red-500">{errors.password.message}</p>} </div> <button type="submit" className="px-4 py-2 bg-green-500 text-white rounded hover:bg-green-600" > Signup </button> </form> </div> );}
2. **Explanation**:

    - `useForm`: Provides hooks for managing form state.
    - `register`: Connects input fields to the form.
    - `handleSubmit`: Handles the form submission.

* * *

#### Advantages of React Hook Form

| Feature | Benefit |
| --- | --- |
| **Performance** | Fewer re-renders with uncontrolled components. |
| **Simple API** | Easy to use and integrate into any project. |
| **Validation** | Built-in support or integration with Yup. |

* * *

### Comparison: Formik vs. React Hook Form

| Feature | Formik | React Hook Form |
| --- | --- | --- |
| **Form State** | Managed internally (controlled inputs). | Uncontrolled inputs for better performance. |
| **Learning Curve** | Simple but more verbose. | Lightweight and concise. |
| **Validation** | Integrates seamlessly with Yup. | Supports Yup and built-in validation. |
| **Performance** | Slightly slower for large forms. | Highly performant. |

* * *

#### Practice Task

1. **Challenge**: Create a contact form using:
    - Name, email, and message fields.
    - Validation for required fields and email format.
    - Use Formik or React Hook Form.

* * *

#### Resources

- [Formik Documentation](https://formik.org/)
- [React Hook Form Docs](https://react-hook-form.com/)
- Learn interactively: [Formik vs. RHF Video](https://www.youtube.com/watch?v=bU_eq8qyjic)