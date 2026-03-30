# Higher-Order Component (HOC)

## 📌 What is this?

A **Higher-Order Component** is a function that takes a component and returns a new component with added or modified behavior. It is a pattern derived from higher-order functions in functional programming.

```ts
const EnhancedComponent = withSomething(WrappedComponent);
```

HOCs do not modify the original component — they wrap it, composing behavior through the component tree.

## 🧠 Core Idea

- A HOC is a **pure function**: same input always produces the same enhanced component
- It injects props, state, or lifecycle behavior into the wrapped component
- The wrapped component remains unaware of the enhancement

## ✅ When to use

- When you need to **reuse cross-cutting logic** across multiple components:
  - logging
  - analytics
  - error boundaries
- When you want to **inject props or behavior** without modifying the original component

---

⚙️ **Example**

```jsx
/* ---------- Wrap Component with HOC ---------- */
const UserInfoWrapper = checkProps(UserInfo);

/* ---------- App ---------- */
export default function App() {
  return (
    <>
      <UserInfoWrapper propA="test1" blabla={{ a: 1, age: 23 }} />
    </>
  );
}

/* ---------- Generic HOC Function ---------- */
export const checkProps = (Component) => {
  return (props) => {
    console.log(props); // added behavior
    return <Component {...props} />; // returns the original component with props
  };
};
```
