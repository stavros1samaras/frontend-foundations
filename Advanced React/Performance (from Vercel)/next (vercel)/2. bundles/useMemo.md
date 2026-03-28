# useMemo usage

## Skipping expensive recalculations

To cache a calculation between re-renders, wrap it in a useMemo call at the top level of your component:

```jsx
import { useMemo } from "react";

function TodoList({ todos, tab, theme }) {
  const visibleTodos = useMemo(() => filterTodos(todos, tab), [todos, tab]);
  // ...
}
```

### You need to pass two things to useMemo:

- A calculation function that takes no arguments, like () =>, and returns what you wanted to calculate.
- A list of dependencies including every value within your component that’s used inside your calculation.

https://react.dev/reference/react/useMemo#skipping-expensive-recalculations

# memo usage

### memo(Component, arePropsEqual?)

Wrap a component in memo to get a memoized version of that component. This memoized version of your component will usually not be re-rendered when its parent component is re-rendered as long as its props have not changed. But React may still re-render it: memoization is a performance optimization, not a guarantee.

```jsx
import { memo } from "react";

const SomeComponent = memo(function SomeComponent(props) {
  // ...
});
```

## Example

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
      <button onClick={parent}>Rerender parent</button>
      <button onClick={child1}>Rerender child1 and parent </button>
      <button onClick={handleprops}>Rerender Children based on props </button>

      {visibleChild}
      <Child2 prop={props} />
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

- **`useMemo`**: Memoizes **values** or **JSX elements** to avoid recalculating them unless dependencies change.
- **`React.memo`**: Wraps a **component** so it only re-renders when its **props** change or internal state change.

### Summary

- Child1 (useMemo): Only re-renders when secondCount changes. Changing props has no effect.
- Child2 (React.memo): Only re-renders when its prop changes. Changing other parent states does not trigger a re-render.
  Parent: Always re-renders when any state inside it changes.
