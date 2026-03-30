# Higher-Order Component (HOC) with TypeScript

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

## ✅ Advantages

- Strong type safety — generics (`T`) preserve the wrapped component’s props
- Prevents prop collisions using `Omit` (consumer cannot override injected props)
- Safer DX — TypeScript catches misuse at compile time
- Clear contract between HOC and wrapped component (what is injected vs expected)
- Scales better than plain HOCs in large codebases with strict typing

---

## ❌ Disadvantages

- More complex syntax — harder to understand for beginners
- Type definitions can become verbose and harder to maintain
- Requires type casting (`as T`) in some cases → slight escape hatch from safety
- Debugging type errors can be non-trivial
- Same architectural downsides as HOCs (wrapper nesting, client-only in Next.js)

---

## 🕐 When to Use

- When building HOCs in a **TypeScript codebase**
- When you need to **inject props safely** without allowing overrides
- When multiple developers consume the same HOC (prevent misuse)
- When correctness and type guarantees are more important than simplicity

---

## 💼 Use Cases

- Injecting controlled props (e.g. `x`, `onMouseMove`, `user`, `theme`) safely
- Building reusable HOCs in design systems or shared libraries
- Preventing consumers from overriding internal logic props
- Complex UI behaviors (mouse tracking, scroll position, viewport data)

---

## ⚠️ Caveats

- **Always use `Omit` for injected props** — prevents accidental overrides
- **Be careful with `as T` casting** — can hide real type issues if misused
- **Keep injected props minimal** — too many increases complexity
- **Prefer hooks when possible** — simpler and easier to type
- **Next.js App Router** — still forces `"use client"` when using HOCs

---

## 📊 Pattern Metrics

| Metric               | Rating                                                      |
| -------------------- | ----------------------------------------------------------- |
| Developer Ergonomics | Medium — safer but more complex syntax                      |
| Flexibility          | High — strong typing with controlled prop injection         |
| Performance          | Medium — same overhead as standard HOCs                     |
| Testability          | High — types make behavior easier to validate               |
| Reusability          | High — reusable and safe across large codebases             |
| Scalability          | Medium — better than plain HOCs, but still limited vs hooks |

## withMouseMoveX

```tsx
export function withMouseMoveX<T extends {}>(
  Component: React.ComponentType<DisplayMousePositionProps>,
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
