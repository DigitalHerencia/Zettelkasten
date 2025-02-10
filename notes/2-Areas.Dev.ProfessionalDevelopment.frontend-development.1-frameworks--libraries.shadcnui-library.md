---
id: jhpa7q3hcr03ma1t5tru7c6
title: shadcnui-library
desc: ''
updated: 1733339868667
created: 1733339790919
---

### Lesson 4: **Shadcn/UI Library**

*(Building accessible, modern, and beautiful UI components effortlessly.)*

* * *

#### What is Shadcn/UI?

- **Definition**: A component library built with **Tailwind CSS** that provides modern, accessible, and reusable UI components.
- **Key Features**:
    - Prebuilt components styled with Tailwind CSS.
    - **Accessibility-first**: Follows WAI-ARIA guidelines for usability.
    - Ready-to-use components for buttons, modals, forms, and more.

* * *

#### Why Shadcn/UI?

| Feature | Benefit |
| --- | --- |
| **Tailwind-compatible** | Seamlessly integrates with your Tailwind CSS project. |
| **Accessible components** | Ensures all users, including those with disabilities, can use your site. |
| **Customizable** | Modify components to suit your design needs. |

* * *

#### Installing Shadcn/UI in a Next.js Project

1. **Setup**:

    - Install the library:

            bashCopy codenpm install shadcn/ui
2. **Configure Tailwind to Work with Shadcn**:

    - Update your `tailwind.config.js` file:

            javascriptCopy codeconst { shadcnPlugin } = require('shadcn/ui'); module.exports = { content: [ "./pages/**/*.{js,ts,jsx,tsx}", "./components/**/*.{js,ts,jsx,tsx}", ], theme: { extend: {}, }, plugins: [shadcnPlugin],};
3. **Restart Your Development Server**:

    - Run `npm run dev` again to apply the changes.

* * *

#### Example: Adding a Button Component

1. **Usage**:

    - In your Next.js project, create a new file `components/Button.js` and add:

            jsxCopy codeimport { Button } from "shadcn/ui"; export default function CustomButton() { return ( <Button variant="primary" className="mt-4"> Click Me </Button> );}
2. **Import and Use the Button**:

    - Update your homepage (`pages/index.js`) to include the button:

            jsxCopy codeimport CustomButton from "@/components/Button"; export default function Home() { return ( <div className="flex flex-col items-center justify-center min-h-screen bg-gray-100"> <h1 className="text-2xl font-bold">Welcome to Shadcn/UI!</h1> <CustomButton /> </div> );}
3. **Result**:

    - You’ll see a styled button with Tailwind's primary theme colors.

* * *

#### Popular Components in Shadcn/UI

| Component | Use Case | Example |
| --- | --- | --- |
| `Button` | Clickable actions | `variant="primary"`, `size="lg"`, `disabled` |
| `Dialog` | Modals for confirmation or forms | `Dialog`, `DialogHeader`, `DialogBody`, `DialogFooter` |
| `Input` | Form inputs like text, email, and passwords | `type="email"`, `placeholder="Enter your email"` |
| `Alert` | Notifications or messages | `variant="success"`, `variant="error"` |
| `Card` | Layout for showcasing content | `Card`, `CardHeader`, `CardBody`, `CardFooter` |

* * *

#### Interactive Activity: Create a Modal (Dialog)

1. **Setup the Dialog**:

    - Create a new file `components/Modal.js`:

            jsxCopy codeimport { Dialog, DialogHeader, DialogBody, DialogFooter } from "shadcn/ui"; export default function Modal({ open, setOpen }) { return ( <Dialog open={open} onClose={() => setOpen(false)}> <DialogHeader> <h2>Welcome to Shadcn/UI</h2> </DialogHeader> <DialogBody> <p>This is an accessible modal created with Shadcn/UI!</p> </DialogBody> <DialogFooter> <button className="px-4 py-2 text-white bg-blue-500 rounded hover:bg-blue-600" onClick={() => setOpen(false)} > Close </button> </DialogFooter> </Dialog> );}
2. **Update the Homepage**:

    - Use the modal in your app:

            jsxCopy codeimport { useState } from "react";import Modal from "@/components/Modal"; export default function Home() { const [open, setOpen] = useState(false); return ( <div className="flex flex-col items-center justify-center min-h-screen bg-gray-100"> <h1 className="text-2xl font-bold">Shadcn/UI Modal Example</h1> <button className="px-4 py-2 mt-4 text-white bg-green-500 rounded hover:bg-green-600" onClick={() => setOpen(true)} > Open Modal </button> <Modal open={open} setOpen={setOpen} /> </div> );}

* * *

#### Challenge: Create a Custom Alert Component

1. Add an **Alert** that:

    - Displays success or error messages.
    - Is dismissible (can be closed with a button).
2. **Hint**: Use `variant="success"` and the `onClose` handler.

* * *

#### Resources:

- [Shadcn/UI Docs](https://shadcn.dev)
- Explore and try components in the Shadcn/UI Component Explorer