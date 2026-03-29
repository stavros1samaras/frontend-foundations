# Errors in JavaScript and React

Errors in JavaScript and React can be categorized based on when and where they occur. Understanding these categories helps in debugging and writing more robust applications.

## 1. JavaScript Errors

JavaScript errors occur during the execution of JS code and can be handled using `try...catch`.

### Common JS Error Types

- **SyntaxError**: Occurs when the code is not valid JavaScript.
- **ReferenceError**: Triggered when accessing an undefined variable.
- **TypeError**: Happens when a value is not of the expected type.
- **RangeError**: Raised when a number is outside an allowable range.
- **EvalError**: Issues related to `eval()` function.
- **URIError**: Errors in URI handling functions (e.g., `decodeURI`).

### Handling JS Errors

```js
try {
  // risky code
} catch (error) {
  console.error(error);
}
```

---

## 2. React Errors

React errors happen during rendering, lifecycle methods, or in components.

### Categories

1. **Render Errors**
   - Occur when a component fails to render.
   - Example: trying to access `props` or `state` incorrectly.

2. **Lifecycle Errors (legacy)**
   - Happen in class component lifecycle methods like `componentDidMount`, `componentDidUpdate`.

### Handling React Errors

- **Error Boundaries** (for class components)
  - Catch render, lifecycle, and child component errors.

```jsx
export class ErrorBoundary extends React.Component {
  state = { hasError: false };

  static getDerivedStateFromError(error) {
    return { hasError: true };
  }

  componentDidCatch(error) {
    console.log("Error: ", error);
  }

  render() {
    if (this.state.hasError) {
      return this.props.fallback;
    }

    return this.props.children;
  }
}
```
