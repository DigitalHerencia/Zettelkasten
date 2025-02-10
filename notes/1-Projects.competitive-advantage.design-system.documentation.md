---
id: vynsh8mbodct28y4pcp0za9
title: documentation
desc: ''
updated: 1722814548794
created: 1722804654736
---

# Templates for Documentation Pages

## Component Documentation Template
### Table of Contents
1. Overview
2. Usage
3. Props
4. Examples
5. Styling
6. Accessibility
7. Best Practices


## 1. Overview
Provide a brief description of the component, its purpose, and where it fits in the design system.

#### Example:

> ### Button Component
>
> > ##### Overview
> > > - The Button component is a fundamental UI element used for triggering actions or events. It supports various styles and states to accommodate different use cases within the application.

---

## 2. Usage
Explain how to import and use the component within a project.

#### Example:

> ### Button Usage
> > To use the Button component, import it from the design system library and include it in your JSX.
> >
> >  ```jsx
> > import { Button } from 'your-design-system';
> >
> > const MyComponent = () => (
> >   <Button variant="primary" onClick={handleClick}>
> >     Click Me
> >   </Button>
> > );
> >  ```

---

## 3. Props
List and describe the props that the component accepts, including their types and default values.

#### Example:

> ### Button Props
> >
> > | Prop Name  | Type     | Default   | Description                                      |
|------------|----------|-----------|--------------------------------------------------|
| `variant`  | string   | 'default' | The style variant of the button (`primary`, `secondary`, `danger`). |
| `size`     | string   | 'medium'  | The size of the button (`small`, `medium`, `large`). |
| `disabled` | boolean  | `false`   | Whether the button is disabled.                  |
| `onClick`  | function | -         | Callback function to handle click events.        |

---

## 4. Examples
Provide example code snippets demonstrating common use cases of the component.

#### Example:
> ### Primary Button
> >```jsx
<Button variant="primary" onClick={handleClick}>
  Primary Button
</Button>
> >
> > ```
> >
> >  ### Secondary Button
> > > ```jsx
<Button variant="secondary" onClick={handleClick}>
  Secondary Button
</Button>
> > >
```
> > >
> > > ### Disabled Button
> > > > ```jsx
<Button variant="primary" disabled>
  Disabled Button
</Button>

> > > > ```

---

## 5. Styling
Explain how to customize the styling of the component, either through props or by overriding default styles.

#### Example:

> ### Button  Styling
> >
The Button component supports several style variants that can be applied via the `variant` prop. Additionally, custom styles can be applied by passing a `className` prop.
> >
> >  ### Using the `variant` prop
> > >```jsx
<Button variant="danger">
  Danger Button
</Button>
> > >```
> > >
> > >  ### Custom Styling
> > > > ```jsx
<Button className="my-custom-button">
  Custom Button
</Button>
> > > >
// CSS
.my-custom-button {
  background-color: purple;
  color: white;
}
> > > > ```

---

## 6. Accessibility
Provide guidelines and best practices for ensuring the component is accessible to all users.

#### Example:
>### Button Accessibility
>>To ensure the Button component is accessible:
>>
>>- Always provide a clear and descriptive `aria-label` if the button text does not convey its purpose.
>>- Avoid using only color to convey state (e.g., use icons or text in addition to color changes).
>>- Ensure the button has sufficient contrast against its background.
>>##### Example:
>>>```jsx
<Button aria-label="Close" variant="secondary">
  <CloseIcon />
</Button>
>>>```

---

## 7. Best Practices
Share tips and best practices for using the component effectively and consistently.

#### Example:
>### Button Best Practices
>>
>> - Use semantic HTML elements (e.g., `<button>`) for buttons to ensure proper behavior across browsers and assistive technologies.
>> - Group related buttons together for better user experience.
>> - Use descriptive text for button labels to improve readability and accessibility.
##### Example:
>>> ```jsx
<div className="button-group">
  <Button variant="primary" onClick={handleSave}>
    Save
  </Button>
  <Button variant="secondary" onClick={handleCancel}>
    Cancel
  </Button>
</div>
>>>```





