# Render Props Pattern

## 📌 What is this?

The **Render Props Pattern** is a design approach where a component provides data or behavior to its children via a function (the "render prop"). Instead of defining UI inside the component, you pass a function that returns JSX, allowing flexible and reusable composition.

This separates **data/logic** from **presentation**, similar to container components, but gives more control to the consumer via a callback.

## 🧠 Core Idea

- The component manages state/fetching internally
- Instead of rendering JSX itself, it calls `render(data)` and returns the result
- The consumer decides what to render — the component only controls the data

## ✅ Advantages

- Separates **logic/state from presentation** cleanly
- Consumer has **explicit control** over rendering output
- Reusable for multiple UIs with the same underlying logic
- Flexible pattern for **data fetching, mouse tracking, resize observers**
- Works seamlessly in both React and Next.js components

---

## ❌ Disadvantages

- Can be verbose with multiple render props or deeply nested components
- Inline render functions may trigger unnecessary re-renders
- Slightly harder to read for beginners compared to simple props
- TypeScript requires careful typing for render function arguments
- Overuse can make JSX less intuitive

---

## 🕐 When to Use

- When multiple components share **the same behavior or data logic**
- When the consumer needs **full control over rendering**
- When you want a **generic, reusable wrapper** component
- When a **children-as-function pattern** is less explicit than a named render prop

---

## 💼 Use Cases

- Data fetching components
- Mouse or viewport position tracking
- Feature toggles / conditional UI based on state
- Generic UI wrappers in design systems
- Animation or timer-driven UI updates

---

## ⚠️ Caveats

- Avoid deeply nested render props for readability
- Always memoize or extract render functions if needed for performance
- Ensure render prop returns valid JSX (single element or fragment)
- TypeScript typing improves safety but adds verbosity
- For Next.js, consider server/client rendering implications

---

## 📊 Pattern Metrics

| Metric               | Rating                                                          |
| -------------------- | --------------------------------------------------------------- |
| Developer Ergonomics | Medium — clear but can be verbose                               |
| Flexibility          | High — consumer controls rendering fully                        |
| Performance          | Medium — inline functions may trigger re-renders                |
| Testability          | High — logic and rendering can be tested separately             |
| Reusability          | High — same logic can be reused with multiple renderers         |
| Scalability          | Medium — works well, but nested render props can reduce clarity |

## ⚙️ Example

```jsx
/* ---------- App ---------- */
export default function App() {
  return (
    <DataSourceWithRenderProps
      getData={() => fetchData("/users/1")}
      render={(resource) => <UserInfo user={resource} />}
    />
  );
}

/* ---------- Generic Render Props Component ---------- */
export const DataSourceWithRenderProps = ({ getData = () => {}, render }) => {
  const [resource, setResource] = useState(null);

  useEffect(() => {
    (async () => {
      const data = await getData();
      setResource(data);
    })();
  }, [getData]);

  return render(resource);
};
```
