---
id: wih40jrsd9ibnuerus4pbtc
title: framer-motion
desc: ''
updated: 1733339868662
created: 1733339830496
---

### Lesson 5: **Framer Motion**

*(Bring your UI to life with animations and interactions.)*

* * *

#### What is Framer Motion?

- **Definition**: A library for creating declarative animations and interactions in React.
- **Key Features**:
    - Animate **elements** with simple syntax.
    - Build **interactive gestures** like drag, hover, and tap.
    - Create **complex animations** with sequences and transitions.
    - Smoothly integrates with React and Next.js.

* * *

#### Why Framer Motion?

| Feature | Benefit |
| --- | --- |
| **Declarative API** | Easy to understand and implement animations. |
| **Gestures** | Add hover, tap, drag, and scroll-based animations. |
| **Performance** | Optimized for 60fps animations. |

* * *

#### Installing Framer Motion in a Next.js Project

1. **Install the Library**:
    - Run:

            bashCopy codenpm install framer-motion

* * *

#### Basic Animation Example

1. **Animating a Box**:
    - Replace `pages/index.js` with:

            jsxCopy codeimport { motion } from "framer-motion"; export default function Home() { return ( <div className="flex items-center justify-center min-h-screen bg-gray-100"> <motion.div className="w-24 h-24 bg-blue-500" animate={{ rotate: 360 }} transition={{ duration: 2, repeat: Infinity }} /> </div> );}
    - **What happens**: The blue box spins in a continuous loop.

* * *

#### Understanding the Code

| Key Prop | Description | Example Value |
| --- | --- | --- |
| `animate` | Defines the end state of the animation. | `{ rotate: 360 }` |
| `transition` | Controls the timing and behavior of the animation. | `{ duration: 2, repeat: Infinity }` |
| `initial` | Sets the initial state before the animation starts. | `{ opacity: 0 }` |

* * *

#### Adding Interactive Gestures

1. **Example: Hover and Tap Effects**:
    - Update your `motion.div` to include gesture props:

            jsxCopy code<motion.div className="w-24 h-24 bg-blue-500" whileHover={{ scale: 1.2 }} whileTap={{ scale: 0.9 }} transition={{ duration: 0.3 }}/>
    - **Result**: The box grows on hover and shrinks when clicked.

* * *

#### Animation Sequences with Variants

1. **Using Variants for Group Animations**:
    - Variants define animation states for elements.
    - Example:

            jsxCopy codeimport { motion } from "framer-motion"; const boxVariants = { hidden: { opacity: 0, x: -100 }, visible: { opacity: 1, x: 0 },}; export default function Home() { return ( <div className="flex items-center justify-center min-h-screen bg-gray-100"> <motion.div className="w-24 h-24 bg-green-500" variants={boxVariants} initial="hidden" animate="visible" transition={{ duration: 1 }} /> </div> );}
    - **Result**: The green box slides in from the left and fades in.

* * *

#### Combining Animations with Gestures

1. **Example: Hover & Drag**:
    - Add a draggable box:

            jsxCopy code<motion.div className="w-24 h-24 bg-red-500" drag whileHover={{ scale: 1.1 }} whileTap={{ scale: 0.9 }}/>
    - **Result**: You can drag the box around, and it scales when hovered or tapped.

* * *

#### Practice Task

1. **Challenge**: Create a "Loading Spinner" that:

    - Rotates a circle continuously.
    - Changes color on hover.
    - Shrinks slightly when clicked.
2. **Hint**: Use `animate`, `whileHover`, and `whileTap`.

* * *

#### Advanced Use Case: Staggered Animations

1. **Animating Multiple Elements**:
    - Example:

            jsxCopy codeconst list = { hidden: { opacity: 0 }, visible: { opacity: 1, transition: { staggerChildren: 0.3 } },}; const item = { hidden: { opacity: 0, y: 20 }, visible: { opacity: 1, y: 0 },}; export default function Home() { return ( <motion.ul className="flex flex-col items-center space-y-4" variants={list} initial="hidden" animate="visible" > <motion.li className="w-24 h-24 bg-blue-500" variants={item} /> <motion.li className="w-24 h-24 bg-green-500" variants={item} /> <motion.li className="w-24 h-24 bg-red-500" variants={item} /> </motion.ul> );}
    - **Result**: Each box appears one after the other in a staggered fashion.

* * *

#### Resources:

- Framer Motion Documentation
- Learn interactively: [Framer Motion Guide](https://motion.dev/)