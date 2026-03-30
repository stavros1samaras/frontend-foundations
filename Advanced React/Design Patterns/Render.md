# Render Props Pattern

## 📌 What is this?

The **Render Props Pattern** is a design approach where a component provides data or behavior to its children via a function (the "render prop"). Instead of defining UI inside the component, you pass a function that returns JSX, allowing flexible and reusable composition.

This separates **data/logic** from **presentation**, similar to container components, but gives more control to the consumer via a callback.

## 🧠 Core Idea

- The component manages state/fetching internally
- Instead of rendering JSX itself, it calls `render(data)` and returns the result
- The consumer decides what to render — the component only controls the data

## ✅ When to use

- When multiple components need the **same data logic but different UIs**
- When you want the consumer to have **explicit, named control** over rendering (vs. the implicit `children` function)
- Good for generic wrappers: data fetching, mouse position tracking, resize observers, etc.

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
