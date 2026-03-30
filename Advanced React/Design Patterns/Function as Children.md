# Function as Children Pattern

## 📌 What is this?

The Function as Children is similar to Render Props, but instead of passing a `render` prop, you pass a function directly as the child. The child function receives data or behavior and returns JSX.

This keeps the JSX cleaner and avoids defining a separate `render` prop.

## 🧠 Core Idea

- The component fetches or manages state
- Passes the data to its **child function**
- The child function returns the UI based on that data
- Eliminates the need for a dedicated `render` prop

## ✅ Advantages

- Clean and explicit pattern for **dynamic UI rendering** based on data or state
- Consumer has **full control** over rendering output
- Avoids creating extra props like `render` — simpler JSX
- Works seamlessly with React and Next.js components
- Flexible for passing multiple values or behaviors to children

---

## ❌ Disadvantages

- Can be less readable if the child function is complex
- Nested or multiple function-as-children components can lead to callback hell
- Slight performance overhead from creating inline functions each render
- Harder to type in TypeScript if multiple arguments are passed
- Can be overkill for simple static children

---

## 🕐 When to Use

- When you need **shared behavior** (mouse tracking, scroll, data fetching) across multiple UIs
- When consumers require **full control over rendering**
- When you want to **avoid HOC wrapper hell**
- When the pattern improves clarity and reduces prop drilling

---

## 💼 Use Cases

- Mouse position tracker: `(coords) => <Component x={coords.x} />`
- Scroll position or viewport tracking
- Data fetching components that render dynamic UIs
- Feature flags where render logic is dynamic per child

---

## ⚠️ Caveats

- Avoid over-nesting function children for readability
- Inline function definitions may trigger unnecessary re-renders
- Ensure returned JSX is a single React element or fragment
- TypeScript requires careful typing for child function parameters
- For Next.js, ensure async data fetching is compatible with server/client boundaries

---

## 📊 Pattern Metrics

| Metric               | Rating                                                                       |
| -------------------- | ---------------------------------------------------------------------------- |
| Developer Ergonomics | Medium — simple for one-off, complex for nested functions                    |
| Flexibility          | High — consumer controls all rendering                                       |
| Performance          | Medium — inline functions can re-render frequently                           |
| Testability          | High — child function can be tested in isolation                             |
| Reusability          | High — component logic reusable with any child function                      |
| Scalability          | Medium — works well for moderate complexity, may get messy with deep nesting |

## ⚙️ Example

```jsx
/* ---------- App ---------- */
export default function App() {
  return (
    <DataSourceWithChildren getData={() => fetchData("/users/1")}>
      {(resource) => <UserInfo user={resource} />}
    </DataSourceWithChildren>
  );
}

/* ---------- Generic Component (children as function) ---------- */
export const DataSourceWithChildren = ({ getData = () => {}, children }) => {
  const [resource, setResource] = useState(null);

  useEffect(() => {
    (async () => {
      const data = await getData();
      setResource(data);
    })();
  }, [getData]);

  return children(resource); // pass data to child function
};
```
