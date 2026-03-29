# React Context

## What is Context?

Context provides a way to pass data through the component tree without manually passing props at every level.

## Key Concepts

### Provider

Holds the data and allows child components to access it.

### Consumer

Used to access the data provided by the Provider.

### useContext Hook

A hook for functional components to read context values directly.

### When to Use Context

- Theme management (light/dark mode)
- User authentication and roles
- Language or localization
- Any global state needed by many components

### Benefits

- Reduces prop drilling
- Makes state accessible to deeply nested components
- Simplifies code for global/shared state

## Example

### context

```tsx
import { createContext } from "react";

export const ThemeContext = createContext("light");
```

### App

```tsx
import { ThemeContext } from "./context";

export default function App() {
  const [theme, setTheme] = useState("light");

  return (
    <>
      <button
        onClick={() =>
          setTheme((prev) => (prev === "light" ? "dark" : "light"))
        }
      >
        change theme
      </button>
      <ThemeContext value={theme}>
        <Box />
      </ThemeContext>
    </>
  );
}

export function Box() {
  const theme = useContext(ThemeContext);
  return <div>{theme}</div>;
}
```
