# `useMemo` vs `React.memo`

## Core Difference

|                    | `useMemo`                       | `React.memo`                               |
| ------------------ | ------------------------------- | ------------------------------------------ |
| **What it is**     | Hook                            | Higher-Order Component (HOC)               |
| **What it caches** | The result of a computation     | The rendered output of a component         |
| **Where it lives** | Inside the parent               | At the child's definition                  |
| **Control**        | You define the dependency array | Automatic shallow compare of props         |
| **Risk**           | Wrong deps → stale values       | Inline objects/functions break memoization |

---

## `useMemo`

Caches the **result** of a computation. Recomputes only when something in the dependency array changes.

```jsx
const visibleChild = useMemo(() => <Child1 prop={props} />, [secondCount]);
```

- `<Child1>` is only recreated when `secondCount` changes.
- If `props` changes, `Child1` **won't see it** — the JSX is stale.
- This is usually a **bug**: you're missing prop updates because you didn't include them in the deps.

> **Use for:** Heavy computations (filtering large arrays, derived data). Not for hiding JSX from React.

---

## `React.memo`

Does a **shallow compare** of props before deciding whether to rerender the component.

```jsx
const Child2 = React.memo(({ prop }) => {
  return <div>child2</div>;
});
```

- If props haven't changed → **skip rerender**.
- If they change → normal rerender.
- Works correctly with primitive props (`number`, `string`, `boolean`).
- **Breaks** with inline objects/functions as props (new reference on every render).

> **Use for:** Components that rerender unnecessarily because their parent rerenders.

---

## Example — what rerenders what

```jsx
import React, { useState, useMemo } from "react";
export default function App() {
  const [count, setCount] = useState(0);
  const [secondCount, setSecondCount] = useState(0);
  const [props, setProps] = useState(0);
  const parent = () => {
    setCount((c) => c + 1);
  };
  const child1 = () => {
    setSecondCount((c) => c + 1);
  };
  const handleprops = () => {
    setProps((c) => c + 1);
  };
  console.log("------------------- \nParent rerenders");
  const visibleChild = useMemo(() => <Child1 prop={props} />, [secondCount]);
  return (
    <>
      <button onClick={parent}>Rerender parent</button>{" "}
      <button onClick={child1}>Rerender child1 and parent </button>{" "}
      <button onClick={handleprops}>Rerender Children based on props </button>{" "}
      {visibleChild} <Child2 prop={props} />{" "}
    </>
  );
}
export function Child1({ prop }) {
  console.log("Child1 with useMemo Rerenders\n-------------------");
  return <div>child1</div>;
}
const Child2 = React.memo(({ prop }) => {
  console.log("Child2 with memo Rerenders\n-------------------");
  return <div>child2</div>;
});
```

### Behavior Table

| Button                           | Parent | Child1 (useMemo)       | Child2 (React.memo)    |
| -------------------------------- | ------ | ---------------------- | ---------------------- |
| Rerender parent                  | ✅     | ❌ deps didn't change  | ❌ props didn't change |
| Rerender child1 and parent       | ✅     | ✅ secondCount changed | ❌ props didn't change |
| Rerender Children based on props | ✅     | ❌ props are stale     | ✅ prop changed        |

> When the **Rerender Children based on props** button is pressed, Child1 misses the `props` update because `useMemo` only watches `secondCount` so Child1 does not rerender. In a prod env this will be considered a bug by the way.

---

## Takeaway

- `React.memo` → the **correct way** to prevent a child from rerendering based on props.
- `useMemo` → for **computations**, not component memoization.
- Wrapping JSX in `useMemo` is an anti-pattern unless you're very careful with your deps.
