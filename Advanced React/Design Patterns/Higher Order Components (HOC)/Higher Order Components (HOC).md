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

## ✅ Advantages

- Reuses cross-cutting logic (logging, analytics, guards) across many components without duplication
- Clean separation of concerns — the wrapped component remains unchanged
- Composable pattern: can be chained (`withAuth(withLogger(Component))`)
- Works across React and Next.js (client components)
- Keeps components focused on UI instead of side logic

## ❌ Disadvantages

- Wrapper hell — deeply nested HOCs make debugging harder in DevTools
- Prop collisions — injected props can silently override existing ones
- Refs are lost unless `React.forwardRef` is used
- Harder TypeScript typing (especially with generics and injected props)
- In Next.js App Router, HOCs force components into **client components**

## 🕐 When to Use

- When you need **shared logic across multiple unrelated components**
- When you want to add behavior without modifying the original component
- When composing multiple behaviors together
- When the logic is **UI-wrapping logic**, not just state logic (otherwise prefer hooks)

## 💼 Use Cases

- Logging / analytics (track renders, props, events)
- Error boundary wrappers
- Feature flags (conditionally render components)

## ⚠️ Caveats

- **Do not create HOCs inside render** — creates a new component each render → full remount
- **Always forward refs** using `React.forwardRef` if needed
- **Set `displayName`** for better DevTools debugging
- **Avoid prop collisions** — namespace or document injected props
- **Next.js App Router** — HOCs force `"use client"`; avoid wrapping server components

---

## 📊 Pattern Metrics

| Metric               | Rating                                               |
| -------------------- | ---------------------------------------------------- |
| Developer Ergonomics | Medium — easy to write, harder to debug              |
| Flexibility          | Medium — composable but risky due to prop collisions |
| Performance          | Medium — adds extra wrapper components               |
| Testability          | Medium — requires testing wrapper + component        |
| Reusability          | High — one HOC can be reused everywhere              |
| Scalability          | Low — becomes hard to manage at scale (prefer hooks) |

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
