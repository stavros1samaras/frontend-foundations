# useCallback (React)

## What it is

A hook that keeps a **stable function reference** between renders.

## Why it matters

Prevents **unnecessary re-renders** when passing functions to child components.

## Usage

### Exaple

```jsx
const fn = useCallback(() => {
  // logic
}, [deps]);
```

### Exaple

```jsx
function Parent() {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => {
    console.log("Clicked!");
  }, []);

  return <Child onClick={handleClick} />;
}

function Child({ onClick }) {
  console.log("Child rendered");
  return <button onClick={onClick}>Click me</button>;
}
```

## Problem

When the child button is clicked, the state changes and the parent rerenders. handleClick now has a new reference, and because it is passed as a prop to the child, the child rerenders too.

## When to use useCallback

- **Passing functions as props to children**  
  Use it when you pass a function to a child and want to avoid **unnecessary re-renders**. Works best with `React.memo`.

- **As a dependency in useEffect or other hooks**  
  If a function is in a dependency array, useCallback keeps a **stable reference** so the effect doesn't run unnecessarily.

- **Performance optimization**  
  Useful when the child component is heavy or many components re-render often due to new function instances.

## When NOT to use useCallback

- No performance issue / child is simple  
  Don’t use it just “in case”—it’s not needed for small, lightweight components.

- The function **isn’t passed as a prop** or **isn’t reused**  
  There’s no risk of unnecessary re-renders in this case.

## Important

- The function **updates only when its dependencies (deps) change**  
  If deps = [], the function stays the same across all renders.
