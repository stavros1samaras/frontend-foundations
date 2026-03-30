# Compound Component Pattern with Context

## 📌 What is this?

The Compound Component pattern allows you to build a parent component with multiple subcomponents that communicate via React Context. This pattern keeps related components together and allows shared state or props without prop drilling.

## 🧠 Core Idea

- Parent creates a **Context provider** and manages shared state
- Child subcomponents consume that context with `useContext`
- Children are exported as **static properties** of the parent (`Select.Option`, etc.)
- Consumers compose children freely in any order inside the parent

## ✅ Advantages

- Enables **shared state** across related subcomponents without prop drilling
- Flexible and composable API — consumers control layout and order freely
- Keeps related components **grouped and maintainable**
- Works seamlessly with both React and Next.js client components
- Encourages **separation of concerns** — parent handles state, children handle presentation

---

## ❌ Disadvantages

- Overhead for simple components — plain props may be simpler
- Extra boilerplate for creating context and subcomponents
- Slight performance cost if many nested consumers re-render frequently
- Requires understanding of React Context API
- Less straightforward for newcomers compared to single component props

---

## 🕐 When to Use

- When multiple related subcomponents need to **share state** internally
- When you want to provide a **flexible, composable API**
- When building UI components with **slots** (header/body/footer)
- When you want to **avoid prop drilling** across nested components

---

## 💼 Use Cases

- Tabs: `<Tabs><Tabs.Tab>…</Tabs.Tab></Tabs>`
- Select / Dropdowns with options: `<Select><Select.Option>…</Select.Option></Select>`
- Accordions: `<Accordion><Accordion.Panel>…</Accordion.Panel></Accordion>`
- Modals with separate header/body/footer slots
- Cards or panels with configurable sections

---

## ⚠️ Caveats

- Can be **over-engineered for simple components**
- React Context updates can trigger re-renders on all consumers
- Requires careful API design for subcomponents
- Not ideal if the component tree is shallow and simple props suffice

---

## 📊 Pattern Metrics

| Metric               | Rating                                                                             |
| -------------------- | ---------------------------------------------------------------------------------- |
| Developer Ergonomics | High — clear separation of state and presentation                                  |
| Flexibility          | High — consumers can compose children freely                                       |
| Performance          | Medium — Context updates may trigger multiple re-renders                           |
| Testability          | High — parent and children can be tested separately                                |
| Reusability          | High — subcomponents are reusable across projects                                  |
| Scalability          | Medium — works well for moderate complexity, may need optimization for large trees |

## ⚙️ Example

```jsx
/* eslint-disable react-refresh/only-export-components */
import { createContext, useContext } from "react";

const Context = createContext(null);

/* ---------- Parent Component ---------- */
export default function CardProvider({ test, children }) {
  return (
    <Context.Provider value={{ test }}>
      <div className="border border-black rounded-md">{children}</div>
    </Context.Provider>
  );
}

/* ---------- Subcomponents ---------- */
function CardBody({ children }) {
  return <div className="p-2">{children}</div>;
}

function CardHeader({ children }) {
  const { test } = useContext(Context);
  return (
    <div className="border-b border-black p-2 mb-2 flex justify-between items-center">
      {children}
      <span>{test}</span>
    </div>
  );
}

function CardFooter({ children }) {
  return (
    <div className="border-t border-black p-2 mt-2 flex justify-end gap-2">
      {children}
    </div>
  );
}

export const Card = {
  Provider: CardProvider,
  Header: CardHeader,
  Body: CardBody,
  Footer: CardFooter,
};
```

### How to use

```jsx
<Card.Provider test="Hello">
  <Card.Header>Title</Card.Header>
  <Card.Body>Content</Card.Body>
  <Card.Footer>Actions</Card.Footer>
</Card.Provider>
```
