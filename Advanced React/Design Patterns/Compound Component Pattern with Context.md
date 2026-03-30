# Compound Component Pattern with Context

## 📌 What is this?

The Compound Component pattern allows you to build a parent component with multiple subcomponents that communicate via React Context. This pattern keeps related components together and allows shared state or props without prop drilling.

## 🤔 Why use it?

- Groups related components (Header, Body, Footer) logically
- Shares state easily between subcomponents using Context
- Keeps UI flexible and composable
- Clean API for consumers

## 🧠 Core Idea

- Create a parent component with a Context provider
- Build child components that consume Context
- Export child components as properties of the parent
- Users can compose the children in any order inside the parent

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
