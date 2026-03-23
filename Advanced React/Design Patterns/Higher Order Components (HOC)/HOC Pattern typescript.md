# Higher-Order Component (HOC) Pattern with TypeScript


## Key TypeScript Concepts

- `T extends {}`: This is a **generic type parameter**. It represents the props of the component that the HOC wraps. Using generics ensures **type safety**, so the wrapped component still gets its own props correctly typed.
  
- `Omit<T, keyof DisplayMousePositionProps>`: This is sometimes called the **TUF pattern** (Type Utility Function). It removes from `T` all keys that are provided by the HOC (`x` and `onMouseMove`) so that the user of the HOC **cannot accidentally overwrite these props**.

- `DisplayMousePositionProps` is the type of props injected by the HOC, in this case:
  ```ts
  interface DisplayMousePositionProps {
    x: number;
    onMouseMove: React.MouseEventHandler;
  }
  ```

## withMouseMoveX
```tsx
export function withMouseMoveX<T extends {}>(
  Component: React.ComponentType<DisplayMousePositionProps>
) {
  return (props: Omit<T, keyof DisplayMousePositionProps>) => {
    const [x, setX] = useState(0);

    const handleMouseMove: MouseEventHandler = (event: MouseEvent) => {
      setX(event.clientX);
    };

    return <Component {...(props as T)} x={x} onMouseMove={handleMouseMove} />;
  };
}
```

## App
```tsx
function App() {
  const Wrapper = withMouseMoveX(DisplayMousePosition);

  return (
    <div className="container">
      <Wrapper />
    </div>
  );
}
```
```jsx
<MouseDisplayWithColor color="red" />; // ✅ Works, 'color' passes correctly
<BrokenComponent x={50} />; // ❌ TypeScript prevents overwriting `x`
```
